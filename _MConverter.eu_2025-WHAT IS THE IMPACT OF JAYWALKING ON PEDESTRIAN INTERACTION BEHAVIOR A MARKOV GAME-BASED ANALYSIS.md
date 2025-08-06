**WHAT IS THE IMPACT OF JAYWALKING ON PEDESTRIAN INTERACTION **

**BEHAVIOR? A MARKOV GAME-BASED ANALYSIS **

by 



Elena Abu Khuzam 



B.A.Sc. in Civil Engineering, The University of Toronto, 2021 



A THESIS SUBMITTED IN PARTIAL FULFILLMENT OF 

THE REQUIREMENTS FOR THE DEGREE OF 



MASTER OF APPLIED SCIENCE 

in 

THE FACULTY OF GRADUATE AND POSTDOCTORAL STUDIES 

\(Civil Engineering\) 



THE UNIVERSITY OF BRITISH COLUMBIA 

\(Vancouver\) 



April 2025 



© Elena Abu Khuzam, 2025 





The following individuals certify that they have read, and recommend to the Faculty of Graduate and Postdoctoral Studies for acceptance, the thesis entitled: WHAT IS THE IMPACT OF JAYWALKING ON PEDESTRIAN INTERACTION 

BEHAVIOR? A MARKOV GAME-BASED ANALYSIS 



submitted by Elena Abu Khuzam 

in partial fulfilment of the requirements for 

the degree of Master of Applied Science 

in 

Civil Engineering 

****

**Examining Committee: **

Dr. Tarek Sayed, Professor, Department of Civil Engineering, UBC 

Supervisor 

Dr. Suliman Gargoum, Assistant Professor, School of Engineering, Civil Engineering, UBCO 

Supervisory Committee Member 



ii 





**Abstract **

Jaywalking behavior represents a major safety concern, especially in traffic environments with intense pedestrian activity. Despite the influence of this behavior on crash risk given that drivers have unexpected interactions with pedestrians and must take additional evasive actions, limited pedestrian models have accounted for jaywalking behavior. This research uses Multiagent Adversarial Inverse Reinforcement Learning \(MAAIRL\) within a Markov game framework to model road user behavior in jaywalking scenarios at signalized intersections, offering a detailed representation of the dynamic and complex decision-making strategies of pedestrians and drivers in these situations. This approach enables obtaining reward functions that can be used to make inferences about their behaviors and optimal policies that represent the actual sequences of decisions, which can be employed in developing microsimulation models. Results show that jaywalking pedestrians exhibited erratic movements, with higher acceleration rates and unpredictable paths. In contrast, non-jaywalking pedestrians showed more predictable behavior with smaller variations in their paths and greater distances from vehicles while crossing. 

Additionally, jaywalking scenarios led to smaller time-to-collision \(TTC\) and post-encroachment time \(PET\) values, reduced minimum distances, and faster pedestrian movements compared to non-jaywalking scenarios, which shows the increased crash risks associated with jaywalking. 

Finally, the MAAIRL model was able to adequately learn the behaviors associated with both non-jaywalking and jaywalking pedestrians. This shows the potential of this framework to model complex real-world scenarios. Moreover, these findings underscore the importance of improving pedestrian simulation models to take into account the distinct behavioral patterns associated with jaywalking, and such advancements can facilitate a more comprehensive examination of the safety impacts in busy pedestrian environments. 

iii 





**Lay Summary **

Jaywalking, i.e., crossing the road when it is not allowed, is a major concern for pedestrian safety, especially in urban areas. Pedestrians who jaywalk often move unpredictably, making it difficult for drivers to react properly and increasing the crash risk. Despite its impact on traffic safety, many current models that study pedestrian behavior do not fully account for jaywalking. 

This study aims to fill that gap by using a machine learning approach to analyze and simulate pedestrian-vehicle interactions at signalized intersections. Their behavior is modeled as a strategic game, where both pedestrians and drivers aim to make the best possible choices based on their goals and the surrounding environment. The findings from this study can be used to improve pedestrian behavior simulations, making them more realistic for traffic safety analysis. 

Improved models can help in designing safer intersections, optimizing traffic signal timings, and developing strategies to minimize dangerous pedestrian-vehicle interactions. 

iv 





## Preface 

Versions of Chapter 3 and Chapter 4 have been submitted for publication, with parts of Chapters 1, 2, and 5 also contributing to the manuscript. I was primarily responsible for the analysis and for writing most of the manuscript. Gabriel Lanzaro was involved in assisting with software code, refining the methodology, and contributing to the validation and revision of the manuscript. Dr. Tarek Sayed, as my research supervisor, provided guidance in the conceptualization, methodology, data collection, and validation of the research. Generative artificial intelligence tools were not used in the research, drafting, or preparation of this thesis. 



****

v 





**Table of Contents **



**Abstract ......................................................................................................................................... iii** **Lay Summary ................................................................................................................................ iv** **Preface ............................................................................................................................................ v** **Table of Contents .......................................................................................................................... vi** **List of Tables ................................................................................................................................. ix** **List of Figures ................................................................................................................................ x** **List of Abbreviations .................................................................................................................... xi** **Acknowledgements ..................................................................................................................... xiv** **Dedication .................................................................................................................................... xvi** **Chapter 1: Introduction ................................................................................................................ 1** 

1.1 

Background ...................................................................................................................... 1 

1.2 

Problem Statement ........................................................................................................... 4 

1.3 

Research Objective .......................................................................................................... 5 

1.4 

Thesis Structure ............................................................................................................... 7 

**Chapter 2: Previous Work ............................................................................................................ 9** 

2.1 

Traditional Road Safety Assessment ............................................................................... 9 

2.2 

Traffic Conflicts ............................................................................................................ 11 

2.2.1 

Traffic Conflict Technique .................................................................................... 11 

2.2.2 

Conflict Indicators ................................................................................................. 13 

2.2.3 

Traffic Conflict Technique Limitations ................................................................. 14 

2.2.4 

Multi-Object Tracking in Computer Vision .......................................................... 15 

vi 





2.2.5 

Applications and Limitations of Microsimulation in Road Safety ........................ 18 

2.3 

Pedestrian Traffic Simulation Models ........................................................................... 21 

2.3.1 

Markov Decision Process ...................................................................................... 23 

2.3.2 

Inverse Reinforcement Learning ........................................................................... 24 

2.3.3 

Multi-Agent Adversarial Inverse Reinforcement Learning ................................... 26 

2.4 

Jaywalking Behavior and Interactions ........................................................................... 27 

**Chapter 3: Methodology ............................................................................................................. 32** 

3.1 

Study Site ....................................................................................................................... 33 

3.2 

Automated Road Safety Analysis .................................................................................. 35 

3.2.1 

Camera Calibration ................................................................................................ 35 

3.2.2 

Road user Detection and Tracking ........................................................................ 36 

3.2.3 

Conflict Detection ................................................................................................. 37 

3.2.4 

Data Extraction Results ......................................................................................... 38 

3.3 

Identifying Behavioral Parameters ................................................................................ 38 

3.4 

Multiagent Modelling .................................................................................................... 41 

3.4.1 

Markov Games \(MGs\) Concept ............................................................................ 42 

3.4.2 

Maximum Entropy Framework ............................................................................. 45 

3.4.2.1 Adversarial Inverse Reinforcement Learning \(AIRL\) ....................................... 46 

3.4.3 

Multiagent Actor-Critic Deep Reinforcement Learning with Kronecker Factors \(MACK\) 48 

**Chapter 4: Results ....................................................................................................................... 50** 

4.1 

Road User Behavioral Characteristics ........................................................................... 50 

4.2 

Reward Functions .......................................................................................................... 56 

vii 





4.3 

Microsimulation Modelling of Actual Behavior ........................................................... 65 

4.3.1 

Performance Evaluation ........................................................................................ 66 

4.3.2 

Trajectory Analysis ............................................................................................... 67 

4.3.3 

Evasive Action Assessment ................................................................................... 70 

4.3.4 

Severity Analysis ................................................................................................... 74 

4.4 

Turning Vehicle Interaction Simulation Model ............................................................ 75 

**Chapter 5: Conclusion ................................................................................................................ 81** 

5.1 

Summary ........................................................................................................................ 81 

5.2 

Contributions ................................................................................................................. 83 

5.3 

Limitations and Future Research ................................................................................... 85 

**Bibliography ................................................................................................................................. 88** 



viii 





**List of Tables **

Table 4.1 Behavioral Parameter Statistics: Mean \(Standard Deviation\) ....................................... 51 

Table 4.2 Normalized Root Mean Square Error \(NRMSE\) Values .............................................. 67 

Table 4.3 Vehicle Confusion Matrix in the Jaywalking Pedestrian-Vehicle Model ..................... 72 

Table 4.4 Pedestrian Confusion Matrix in the Jaywalking Pedestrian-Vehicle Model ................. 72 

Table 4.5 Vehicle Confusion Matrix in the Non-Jaywalking Pedestrian-Vehicle Model ............. 73 

Table 4.6 Pedestrian Confusion Matrix in the Non-Jaywalking Pedestrian-Vehicle Model ......... 73 

Table 4.7 Simulated Pedestrian-Vehicle Right-Turn Interactions Behavioral Statistics ............... 80 



ix 





**List of Figures **

Figure 2.1 Safety Pyramid \(adapted from Laureshyn and Varhelyi, 2018\) .................................. 13 

Figure 3.1 Pedestrian-Vehicle Interactions Modeling Framework ............................................... 33 

Figure 3.2 Site Location: East Hastings Street & Main Street Intersection .................................. 34 

Figure 3.3 Automated Conflict Analysis ....................................................................................... 35 

Figure 3.4 Road users' lateral distance, longitudinal distance, interaction angle, and heading angle .............................................................................................................................................. 41 

Figure 4.1 Pedestrian Behavioral Parameters ................................................................................ 54 

Figure 4.2 Vehicle Behavioral Parameters .................................................................................... 56 

Figure 4.3 Speed Difference and Interaction Angle ...................................................................... 56 

Figure 4.4 Reward Functions for Jaywalking Pedestrian-Vehicle Interactions ............................ 63 

Figure 4.5 Reward Functions for Non-Jaywalking Pedestrian-Vehicle Interactions .................... 65 

Figure 4.6 Trajectory Simulations for Pedestrian-Vehicle Interactions ........................................ 69 

Figure 4.7 Conflict Severity PET Distribution Simulation Comparison ....................................... 74 

Figure 4.8 Conflict Severity TTC Distribution Simulation Comparison ...................................... 75 

Figure 4.9 Simulated Pedestrian-Vehicle Right-Turn Scenarios .................................................. 76 

Figure 4.10 Simulated Pedestrian-Vehicle Right-Turn Interactions Distributions ....................... 79 



x 





**List of Abbreviations **

ABM 

Agent-Based Model 

AIRL 

Adversarial Inverse Reinforcement Learning 

APC 

Autonomous Pedestrian Crossing 

AVs 

Autonomous Vehicles 

CA 

Cellular Automata Model 

CAVE 

Cave Automatic Virtual Environment 

CC 

Camera Calibration 

CF 

Car-Following Model 

CMFs 

Crash Modification Factors 

CPI 

Crash Potential Index 

CV 

Computer Vision 

DBN 

Dynamic Bayesian Networks 

DCM 

Discrete Choice Model 

DPRF 

Distracted Pedestrian Reward Function 

DRAC 

Deceleration Rate to Avoid a Crash 

DRL 

Deep Reinforcement Learning 

DVRF 

Vehicle Reward Functions in Distracted Scenarios 

ETC 

Electronic Toll Collection 

FM 

Feature Matching 

GANs 

Generative Adversarial Networks 

GCL 

Guided Cost Learning 

xi 





GP-IRL 

Gaussian Process Inverse Reinforcement Learning 

GT 

Gap Time 

HRC 

Hybrid Retraining Constrained training technique 

ICBC 

Insurance Corporation of British Columbia 

IKKW 

Improved Kerner-Klenov-Wolf Model 

IRL 

Inverse Reinforcement Learning 

KLT 

Kanade-Lucas-Tomasi Feature-Tracking Algorithm 

LC 

Lane-Changing 

LSBRE 

Logistic Stochastic Best Response Equilibrium 

LSTM 

Long Short-Term Memory neural networks 

MA-AIRL Multi-Agent Adversarial Inverse Reinforcement Learning Multi-Agent Actor-Critic Deep Reinforcement Learning with MACK 

Kronecker factors 

MARL 

Multi-Agent Reinforcement Learning 

MDP 

Markov Decision Process 

ME 

Maximum Entropy 

MFC 

Free-Flow Acceleration Model 

MG 

Markov Games 

NPRF 

Non-distracted Pedestrian Reward Function 

NRMSE 

Normalized Root Mean Square Error 

NVRF 

Vehicle Reward Functions in Non-distracted Scenarios 

O-D 

Origin-Destination 

xii 





PET 

Post-Encroachment Time 

PFG 

Pedestrian Flashing Green 

RL 

Reinforcement Learning 

RNNs 

Recurrent Neural Networks 

RTTC 

Relative Time-to-Collision 

SFGM 

social group force model 

SFM 

Social Force Model 

SPFs 

Safety Performance Functions 

SSM 

Surrogate Safety Measures 

TCT 

Traffic Conflict Technique 

TTC 

Time-to-Collision 

UAVs 

Unmanned Aerial Vehicles 

UBC 

University of British Columbia 





xiii 





## Acknowledgements 

I would like to express my deepest gratitude to my supervisor, Dr. Tarek Sayed, for his invaluable guidance, support, and encouragement throughout this research journey. I feel incredibly fortunate to have had the opportunity to learn from him, not just in the technical aspects of my work, but in the way he approaches challenges with curiosity, dedication, and an unrelenting passion for the field. 

I also want to extend my sincere appreciation to Gabriel. Your patience, kindness, and willingness to share your knowledge have been invaluable throughout this process. From navigating challenges in my research to offering thoughtful advice, your support has made a significant impact on both my academic growth and personal confidence. More than just a mentor, you’ve been a steady source of encouragement, and I am truly grateful for that. 

To my colleagues and friends at UBC and the research lab, thank you for the engaging discussions, collaboration, and support throughout this process. Your encouragement and friendship have made this journey so enjoyable and meaningful. 

A special thanks to my family, whose unwavering love and support have been the foundation of everything I have accomplished. To my parents, Shadi and Sara, thank you for always believing in me and for instilling in me the values of perseverance, hard work, and curiosity. Your sacrifices and endless encouragement have shaped the person I am today. No words can truly capture how grateful I am for your unconditional love and support. To my sister, Sandra, thank you for your constant support, for cheering me on, and for always being there through everything. No matter the distance, your love has been a source of strength for me. 

xiv 





To Amir, my rock and my greatest supporter, words cannot fully express my gratitude for your love, patience, and encouragement throughout this journey. Your constant belief in me, even when I doubted myself, has meant everything. Thank you for always being there, for reminding me to take breaks when I needed them, and for celebrating even the smallest victories with me. I am so grateful to have you by my side, and I cannot wait for the next chapter of our lives together. 

This thesis is a culmination of the support, knowledge, and kindness of so many people, and I am truly thankful for each and every one of you. 

xv 





## Dedication 

*To my beloved parents, sister, and fiancé. *

xvi 





## Chapter 1: Introduction 

This chapter introduces this research, including a background on jaywalking and its impact on pedestrian safety. Then, this chapter contains the problem statement and the research objectives, which highlight the contributions of the study. Finally, the structure of the thesis is provided. 

**1.1 Background **

Road safety remains a pressing global issue, especially for vulnerable road users \(VRUs\) such as pedestrians, cyclists, and motorcyclists, who are disproportionately affected by traffic-related incidents. The World Health Organization \(WHO\) reports that road traffic crashes cause approximately 1.3 million deaths each year, with VRUs accounting for over half of these fatalities \(WHO, 2023a\). In response to the growing concern, the United Nations \(UN\) declared the First Decade of Action for Road Safety from 2011–2020, aiming to stabilize and then reduce the anticipated level of global road traffic fatalities \(UNECE, 2021\). Despite this initiative, the targets were not fully met, and a second decade, the Decade of Action for Road Safety 2021–

2030, was adopted in August 2020 through UN General Assembly resolution 74/299. This new decade sets a more ambitious goal: to prevent at least 50% of road traffic deaths and injuries by 2030. 

The Second Decade places a strong emphasis on improving safety for vulnerable road users, recognizing their significant role in the global road safety crisis. Pedestrians, in particular, face heightened risks in traffic environments, with global pedestrian deaths representing about 23% of all road traffic fatalities \(WHO, 2023a\). In the United States, the situation has worsened: between 2008 and 2018, pedestrian deaths increased by 41%, while fatalities among other road 1 





users only saw a modest decline of 7%. This sharp rise in pedestrian deaths reflects the increasing number of vehicles on the roads, as well as urban infrastructure that often prioritizes motorized traffic over pedestrian safety. Road traffic injuries are now the leading cause of death among children and young adults aged 5–29 years, underlining the vulnerability of pedestrians in particular. 

Moreover, road traffic fatalities are not evenly distributed worldwide. Approximately 92% of global road traffic deaths occur in low- and middle-income countries, which together account for only about 60% of the world’s vehicles \(WHO, 2023b\). This stark discrepancy highlights the fact that infrastructure in these regions tends to prioritize the flow of motorized traffic, often at the expense of pedestrian safety. Combined with insufficient safety measures, this imbalance places pedestrians at heightened risk, especially in densely populated urban environments. 

Traditional road safety studies have relied on crash data collected from police reports, hospital records, and insurance claims \(Elvik & Mysen, 1999; World Health Organization, 2018\). 

However, this reactive approach has several limitations, including underreporting, data inconsistencies, and the inability to provide a real-time understanding of pedestrian-vehicle interactions. Research suggests that pedestrian crashes are significantly underreported in official records, particularly in cases involving minor injuries or near-miss incidents \(Andrade Lanzaro, 2021; Leur & Sayed, 2001; Nasernejad et al., 2021a; Sayed & Zein, 1999; Zheng et al., 2021\). 

Recent advancements in road safety analysis have shifted toward using surrogate safety measures \(SSMs\), such as traffic conflicts, to assess safety risks in real time. Unlike crash data, SSMs enable the identification of potential conflicts before they escalate into actual crashes, allowing for proactive safety interventions \(Ismail et al., 2010; Saunier & Sayed, 2006, 2007\). 

2 





Advancements in artificial intelligence \(AI\) and computer vision technologies have further enhanced the ability to analyze pedestrian behavior and traffic conflicts. Automated video analysis and deep learning techniques have enabled researchers to model pedestrian movements more accurately, capturing decision-making processes and predicting interactions with vehicles. 

AI-based simulation models, including microsimulation, agent-based modeling \(Jennings, 2000\), and reinforcement learning approaches \(Littman, 1994; Puterman, 1990\) offer promising avenues for understanding pedestrian behavior in dynamic traffic environments. Recent research has increasingly emphasized the need for a deeper, data-driven understanding of pedestrian decision-making. Advancements in AI and multiagent modeling offer new opportunities to analyze pedestrian behavior more accurately. 

However, one pedestrian behavior that remains insufficiently understood is jaywalking. 

Jaywalking, a form of non-compliant pedestrian behavior, remains a significant contributor to pedestrian crashes. Studies indicate that nearly 37% of pedestrian crashes in urban environments are linked to jaywalking \(Choi et al., 2013\), with pedestrian behavioral factors accounting for approximately 59% of vehicle-pedestrian collisions \(Ulfarsson et al., 2010\). Despite widespread recognition of its risks, jaywalking persists, particularly in dense urban areas where high pedestrian volumes and infrastructure constraints often create conditions that encourage noncompliance. While enforcement and road design play a role in shaping pedestrian behavior, traditional safety measures often fail to fully address the underlying factors that lead to jaywalking. 

3 





**1.2 Problem Statement **

While pedestrian safety has been the subject of numerous studies, jaywalking remains a critical and understudied behavior that significantly contributes to pedestrian crashes. Despite its prevalence, the underlying mechanisms of jaywalking and its interaction with vehicles are not well understood. Traditional safety analysis methods that rely on crash data do not adequately capture the complexity of pedestrian decision-making or the real-time collision avoidance mechanisms employed by both pedestrians and drivers. The shift towards using surrogate safety measures, such as traffic conflicts, offers a more effective approach for understanding pedestrian-vehicle interactions. However, existing pedestrian behavior models still struggle to accurately represent jaywalking behavior and its impact on road safety. 

Moreover, research on jaywalking across various environments suggests that multiple factors influence this type of behavior. In addition to environmental and infrastructural elements, such as signal timing and pedestrian amenities, social and psychological factors, including impatience and group behavior, can contribute to jaywalking \(Bansal et al., 2022; H. Guo et al., 2012; B. Li, 2013\). Some studies have shown that pedestrians tend to jaywalk when they perceive minimal conflict risks or when they face long wait times at traffic signals \(H. Guo et al., 2012\). Moreover, group behavior often leads to more frequent violations, as individuals may follow the actions of others in their vicinity \(Russo et al., 2018\). 

Recent advancements in AI and machine learning have opened new opportunities for modeling pedestrian behavior in dynamic traffic environments. AI-driven techniques, including reinforcement learning and inverse reinforcement learning, have demonstrated potential in replicating real-world decision-making processes. However, current research lacks a robust 4 





framework for integrating these advanced techniques with pedestrian safety analysis, particularly in the context of jaywalking. Existing studies, such as Hussein and Sayed \(2019\), have developed agent-based models for pedestrian simulation, but they do not account for jaywalking behavior. While multiagent learning approaches offer the potential for capturing interactions between pedestrians and drivers, they have not yet been applied to simulate jaywalking specifically \(Alsaleh & Sayed, 2021a; Nasernejad et al., 2023\). This gap limits our ability to effectively simulate non-compliant pedestrian behavior and its influence on vehicle responses, limiting their applicability in road safety studies. 

The problem addressed in this research is the need for a more realistic modeling approach that accurately represents jaywalking behavior and pedestrian-vehicle interactions. Accurate models of jaywalking behavior are crucial for predicting pedestrian-vehicle conflicts and developing proactive measures that can reduce the incidence of crashes and fatalities. By using AI-based simulation techniques and surrogate safety measures, this study aims to bridge the gap between traditional pedestrian safety analysis and emerging computational methods. By integrating advanced techniques, researchers can better understand and predict jaywalking behavior, optimize infrastructure design, and implement proactive interventions to reduce pedestrian-vehicle conflicts. 

**1.3 Research Objective **

The objective of this research is to analyze and simulate the behavior of jaywalking pedestrians during interactions with vehicles and to compare their behavior with non-jaywalking pedestrians. 

This study aims to achieve the following objectives: \(1\) Identify key behavioral differences between jaywalking and non-jaywalking pedestrians in conflict scenarios, \(2\) Develop a data-5 





driven model to capture pedestrian-vehicle interactions and road user decision-making, \(3\) Evaluate the influence of road user intentions and external factors on jaywalking behavior, and \(4\) Assess potential safety interventions to mitigate conflicts at signalized intersections. 

To achieve these objectives, this study applies a multiagent learning framework to model pedestrian-vehicle interactions, recognizing that both pedestrians and drivers act as decision-makers with conflicting preferences. By capturing the underlying reward structures and intentions of jaywalking pedestrians and drivers during conflicts, the study provides insights into proactive safety measures that can anticipate and mitigate risks associated with jaywalking. The proposed models are validated using real-world data to ensure their applicability in predictive safety assessments. 

This study makes several key contributions to the literature on pedestrian safety and modeling, particularly regarding jaywalking behavior. First, it systematically differentiates pedestrian-vehicle conflicts involving jaywalking and non-jaywalking pedestrians, highlighting behavioral variations that are often overlooked in traditional models. Second, by applying a multiagent learning approach, this study provides a transferable framework for understanding pedestrian and driver decision-making \(Alsaleh & Sayed, 2021a; Alsharif et al., 2024; Nasernejad et al., 2023\). 

Third, it evaluates the potential for optimizing signal timings and other safety interventions based on the identified behavioral patterns. Practical applications include designing safer signalized intersections by simulating pedestrian-vehicle interactions in environments where jaywalking is prevalent and assessing the effectiveness of intervention strategies. By integrating jaywalking-specific analyses into multiagent frameworks, the study contributes to the advancement of 6 





pedestrian modeling, offering actionable insights to prioritize safety while accommodating diverse and unpredictable pedestrian behaviors. 

**1.4 Thesis Structure **

This thesis is organized into five chapters: introduction, previous work, methodology, results, and conclusions. 

Chapter 1 introduces the background and importance of pedestrian safety, focusing on issues like jaywalking and its role in pedestrian-vehicle conflicts. It highlights the need for improved road safety measures, especially at signalized intersections where jaywalking occurs. This chapter outlines the problem statement, research objectives, and the structure of the thesis. It lays the foundation for the research by providing context on the challenges pedestrians face and the methods used to study their behavior. 

Chapter 2 provides an overview of existing research related to road safety, with a focus on pedestrian behavior, traffic conflicts, and jaywalking. It reviews traditional methods of analyzing road safety, such as crash data, and discusses how new techniques, such as surrogate safety measures and traffic conflict techniques, can be used to assess pedestrian-vehicle interactions more proactively. The chapter also explores previous studies on pedestrian behavior, specifically jaywalking, and the factors influencing these behaviors. It highlights key models used to study pedestrian movement and interactions with vehicles. 

Chapter 3 outlines the research design and methodology used in the study. It describes the study sites, the process of automated video analysis for identifying pedestrian-vehicle conflicts, and the 7 





application of reinforcement learning techniques to model pedestrian behavior. This chapter also introduces multiagent modeling approaches to simulate complex pedestrian-vehicle interactions. 

Chapter 4 presents the findings of the research, offering a comparative analysis of behaviors exhibited by jaywalking pedestrians and non-jaywalking pedestrians. It analyzes the utility functions derived from the modeling process, providing insights into the decision-making frameworks of pedestrians and drivers during conflicts. Simulation models replicating real-world behaviors are shown, including scenarios involving right-turn movements, to illustrate the dynamics of pedestrian-vehicle interactions and the efficacy of the proposed models in capturing these complexities. The final chapter, Chapter 5, summarizes the research findings, discussing their implications in the context of pedestrian safety. It highlights the contributions of the study to existing knowledge, acknowledges limitations encountered during the research, and proposes recommendations for future studies. 



8 





## Chapter 2: Previous Work 

This chapter presents a comprehensive literature review that synthesizes current research on jaywalking behaviors and explores methodologies to model pedestrian-vehicle interactions. The first section shows an overview of traditional safety analysis. The second section examines advancements in traffic conflict techniques, followed by computer vision techniques for safety assessment. The third section reviews studies in traffic simulation models, particularly focusing on artificial intelligence algorithms and their applications in simulating pedestrian-vehicle interactions. It includes Agent-Based Modeling, Markov Decision Processes \(MDPs\), Deep Reinforcement Learning, and Inverse Reinforcement Learning techniques utilized in previous traffic simulation models. The final section provides a comprehensive review of various studies surrounding jaywalking behavior and its influence on pedestrian-vehicle interactions. 

**2.1 Traditional Road Safety Assessment **

Traditional road safety studies focus on analyzing historical crash data to identify locations with greater crash occurrences. This data is predominantly obtained from police reports and potentially enhanced with data from hospitals and insurance claims to obtain a more comprehensive understanding of the nature and severity of crashes \(Brubacher et al., 2019; Sayed & Zein, 1999\). The traditional approach primarily involves the development of safety performance functions \(SPFs\) and crash modification factors \(CMFs\) to assess road safety. SPFs are equations that predict the number of crashes by relating them to explanatory variables such as traffic volume, road geometry, and zonal characteristics. Developing SPFs typically requires collecting crash data over three years \(El-Basyouny, 2011; Sacchi & Sayed, 2016\). Additionally, CMFs represent the effectiveness of safety interventions \(e.g., lane widening, pavement 9 





markings\) in reducing crashes \(Hauer et al., 2012\). A CMF value lower than one indicates a reduction in crashes, while values equal to or greater than one suggest no change or an increase in crash risk \(AASHTO, 2010\). 

Despite their widespread use, traditional crashes datasets, particularly derived from police reports, face several challenges that compromise their reliability. These challenges include underreporting, inaccuracies in record-keeping, and inconsistencies in data collection methods across different regions \(Andrade Lanzaro, 2021; Leur & Sayed, 2001; Nasernejad et al., 2021a; Sayed & Zein, 1999; Zheng et al., 2021\). Regional variations also exist in crash reporting, which is influenced by local regulations and legal frameworks, and this further exacerbates these discrepancies. The rarity and randomness of crashes also present a significant limitation. Since crashes are relatively infrequent events compared to exposure \(traffic volume\), data must be collected over long periods to provide statistically reliable results \(Andrade Lanzaro, 2021; Autey et al., 2012; Sayed & Zein, 1999; Zheng et al., 2021\). This delay not only postpones safety improvements but also raises ethical concerns, as it relies on crash occurrence, including fatalities, to identify hazardous locations. Furthermore, the road environments are dynamically shaped by changes in user behavior, land use, and emerging technologies like autonomous vehicles and micromobility, which further complicates the fast and immediate identification of crash-prone zones. 

To address these challenges, researchers are increasingly adopting proactive strategies that move beyond reactive crash-based analyses. One promising direction is the use of surrogate safety measures \(SSMs\), which evaluate safety using frequently observed interactions that almost lead to crashes instead of waiting for these crashes to occur. Traffic conflicts, one of the most utilized 10 





SSMs, provide valuable insights into the crash contribution factors, which can be effective for interventions that aim to mitigate some types of behavior \(e.g., sudden crossings, prohibited movements\). Other SSMs include non-compliance with design standards, deceleration rates, and the number of vehicles in dilemma zones \(Gettman et al., 2003; Richl & Sayed, 2006\). 

**2.2 Traffic Conflicts **

Traffic conflicts are an essential aspect of transportation safety analysis, as they provide insights into potential crashes. This subsection explores the methods used to detect and analyze traffic conflicts, as well as the various techniques and indicators to assess their severity, the limitations of the traffic conflict technique, and the applications of microsimulation models and computer vision technologies with this regard. 

**2.2.1 Traffic Conflict Technique **

Traffic conflicts can be defined as situations where road users nearly collide but they take evasive maneuvers like braking or swerving \(Amundsen & Hydén, 1977; Andrade Lanzaro, 2021; Ghoul, 2021; Perkins & Harris, 1968; Zheng et al., 2021\).These conflicts are critical in safety studies as they offer insights into the factors contributing to crashes. Unlike traditional crash data, which requires significant time to accrue and analyze, traffic conflicts provide a more immediate and proactive approach to identifying potential crash-prone areas. 

Various methods are employed to collect data on traffic conflicts \(Zheng et al., 2014\), including field observations where trained observers monitor interactions on-site or through video analysis. 

While manual observation may be subjective and labor-intensive, automated video analysis and data from autonomous vehicle sensors provide more objective and detailed insights into road 11 





user behavior. Naturalistic driving studies, where vehicles are equipped with sensors to capture driving maneuvers, behavior, and environmental conditions over time, also offer valuable insights into evasive actions in normal and conflict situations. Simulation models like VISSIM 

and AIMSUN also simulate traffic conflicts after adjusting parameters to match real-world conditions \(Huang et al., 2013\). By accelerating the identification of potential collision risks, traffic conflicts offer an efficient and cost-effective approach that minimizes risks to human life. 

This proactive method not only reduces data collection times from years to weeks or days but also allows safety engineers to implement preemptive measures to enhance road safety based on real-time insights. 

Hydén \(1987\) proposed a hierarchical severity framework for traffic conflicts to illustrate their varying degrees of risk. This framework emphasizes that not all conflicts are equally hazardous: this pyramid-shaped hierarchy categorizes interactions from minor incidents at the base to potential collisions at the apex, which illustrates the spectrum of severity based on frequency and potential impact, as depicted in Figure 2.1. 



12 





Crashes



**Figure 2.1 Safety Pyramid \(adapted from Laureshyn and Varhelyi, 2018\)** **2.2.2 Conflict Indicators **

Conflict indicators provide an objective framework to evaluate the severity of interactions between road users by quantifying their spatial and temporal proximity. These metrics aim to minimize subjectivity in assessing conflicts and enable data-driven evaluations. Among the commonly used indicators, the Time-to-Collision \(TTC\) calculates the remaining time before a collision occurs if vehicles maintain their current speeds and trajectories. Initially proposed by Hayward \(1972\), TTC has become a cornerstone in conflict analysis due to its ability to encapsulate both spatial and temporal proximity. Shorter TTCs indicate higher collision risks, making it a crucial metric for proactive safety assessments, particularly at intersections and high-speed roadways \(Zaki et al., 2016\). Similarly, the Post-Encroachment Time \(PET\) assesses the time difference between the exit of one road user from a conflict point and the arrival of another at the same location \(Allen et al., 1978; Minderhoud & Bovy, 2001\). PET is widely applied at intersections, crosswalks, and merging zones, with lower PETs reflecting higher severity. 

Another important metric, Gap Time \(GT\), measures the time interval between two vehicles 13 





entering an area, making it particularly useful for analyzing merging conflicts on road segments like highway on-ramps. A shorter GT means a higher likelihood of severe conflict due to the reduced time for vehicles to adjust their speeds or positions. 

Another critical measure is the Deceleration Rate to Avoid a Crash \(DRAC\), which quantifies the rate of deceleration required by a vehicle to avoid a collision \(Gettman et al., 2003\). CPI, which is based on DRAC, is a related metric used in simulation models to reflect the urgency of driver reactions and road conditions \(Cunto & Saccomanno, 2008\). A higher DRAC indicates a more severe conflict scenario. Similarly, the Proportion of Stopping Distance \(PSD\) evaluates the minimum distance between vehicles during a conflict, expressed as a proportion of the distance required to stop safely \(Gettman et al., 2003\). This measure is essential for identifying rear-end collision risks and assessing following distance issues, as it accounts for both speed and braking capabilities. 

The severity of these conflicts may be further evaluated using additional factors such as the magnitude of the evasive actions, including braking intensity and steering adjustments, as well as the proximity between road users \(Zheng et al., 2021\). These metrics are tailored to the specific characteristics of each conflict, taking into account the type of road users involved and the nature of the crash, such as rear-end, sideswipe, or intersection-related incidents. 

**2.2.3 Traffic Conflict Technique Limitations **

Traffic conflict techniques for safety assessments offer several advantages. First, traffic conflicts occur more frequently than collisions, enabling more data for analysis. This higher occurrence rate significantly reduces data collection time compared to waiting for collisions to happen. 

14 





Additionally, the social and economic costs of collecting traffic conflict data are much lower than those associated with collision data, which addresses the ethical dilemma of waiting for collisions to conduct sound safety diagnoses. Finally, conflicts offer valuable insights into the contributing factors of collisions and facilitate before-and-after studies to evaluate the effectiveness of safety interventions. 



Despite these benefits, previous studies have highlighted some drawbacks \(Chin & Quek, 1997\). 

The primary issues arise from the subjectivity involved in defining and collecting traffic conflict data. Differentiating between evasive actions and normal behavior can be challenging, as not all braking and swerving maneuvers are evasive. Additionally, various studies have used different thresholds to define conflicts, leading to inconsistencies in identification. These thresholds may be based on conflict indicator values, but there is no universally accepted standard, making comparisons across studies difficult \(Svensson, 1998\). Moreover, manual data collection is prone to inaccuracies due to human factors such as observer inexperience, inconsistent interpretations, and fatigue. However, the errors associated with human factors can be mitigated through video analysis techniques, which offer a more objective and reliable means of data collection. 

**2.2.4 Multi-Object Tracking in Computer Vision **

Manually collecting traffic conflict data can be challenging, unreliable, labor-intensive, and time-consuming. Recent advancements in computer vision \(CV\) have considerably improved conflict detection by employing automated video analyses, which has significantly enhanced the efficiency, accuracy, and reliability of safety assessments. Many studies have successfully applied computer vision for automated video analysis and conflict identification, achieving 15 





accuracy rates of approximately 90% \(Saunier & Sayed, 2006; Zaki et al., 2016\). At UBC, the process begins with camera calibration, which establishes a relationship between 2D video coordinates and real-world 3D coordinates using a homography matrix \(Ismail et al., 2013\). This calibration aligns the video footage with real-world distances, angles, and perspectives through point correspondences, distance constraints, angular constraints, and equidistance constraints. 

After calibration, multi-object tracking is applied to detect and monitor road users over time. 

Clustering techniques are then used to analyze patterns of movement and identify interactions relevant to traffic safety assessments. 



Multi-object tracking \(MOT\) is a pivotal area in computer vision, enabling the identification and monitoring of multiple objects within a scene \(Wojke et al., 2017\). This capability is particularly valuable in transportation research, where real-time road user tracking is essential for assessing safety and mobility. Algorithms such as YOLOv8 and BoTSORT have been instrumental in developing MOT methodologies, offering solutions to common challenges such as occlusions, crowded environments, and computational efficiency \(Jin, 2024; T. Li, Li, et al., 2023\). 

YOLOv8 \(You Only Look Once version 8\) is a deep learning algorithm designed for fast and accurate object detection. It is known for processing images and identifying multiple objects in a scene, which is particularly useful for tracking multiple road users in traffic environments. 

DeepSORT \(Simple Online and Real-time Tracking with a Deep Association Metric\) is a deep learning-based enhancement of the SORT algorithm that incorporates appearance features to improve occlusions and re-identifications issues \(Wojke et al., 2017\). Widely used for MOT, DeepSORT combines motion models using Kalman filtering and appearance models derived from deep feature extraction. This approach effectively reduces identity switches and enhances 16 





tracking accuracy. However, its performance can be challenged in highly crowded or dynamic environments with frequent occlusions. BoTSORT, a newer algorithm, builds on the limitations of DeepSORT by incorporating advanced data association methods and more sophisticated feature embedding techniques \(T. Li, Li, et al., 2023\). Its application in transportation analysis has shown improved accuracy in tracking pedestrian movements and vehicle interactions. 

Several studies have demonstrated the effectiveness of MOT algorithms in transportation contexts, particularly for analyzing road user interactions and identifying conflict points. For instance, Zaki & Sayed \(2013\) developed an automated video-analysis-based system to track and analyze cyclist behavior, identifying key traits such as speeds, travel paths, and conflict points. 

Similarly, Alsaleh et al. \(2018\) employed computer vision techniques to examine the effects of pedestrian distraction at crosswalks by capturing trajectories and deriving gait-related metrics such as step length, step frequency, and walking stability. These studies highlight the potential of MOT algorithms to enhance safety assessments and risk evaluation in urban environments. 

Recent advancements in MOT have also emphasized the use of raw images to improve detection accuracy and reduce computational overhead. Studies have shown that raw images for training, when used with algorithms like YOLOv8 and BoTSORT, retain more unprocessed scene information, allowing for more detailed recognition of objects, which leads to more accurate tracking of road users, while reducing the need for complex image signal processing \(ISP\) pipelines \(Jin, 2024\). This approach ameliorates real-time object detection workflows, reducing computational costs and improving the feasibility of deploying these systems for traffic monitoring and autonomous driving applications. Additionally, BoTSORT's performance has been validated across multiple datasets, such as MOT20, where it achieved superior tracking 17 





accuracy compared to previous algorithms like YOLO-DeepSORT. Notably, it demonstrated better performance in scenarios with dim lighting and crowded areas, maintaining road users’ 

identifications and minimizing tracking errors \(T. Li, Li, et al., 2023\). 

**2.2.5 Applications and Limitations of Microsimulation in Road Safety** Microsimulation models offer several advantages for traffic safety, particularly in evaluating the effects of design changes without physically implementing them. By eliminating the need for costly and time-intensive before-and-after studies, these models provide a cost-effective alternative. Additionally, they address limitations associated with video-based conflict data collection, such as high computational and labor costs. For instance, tools like the Surrogate Safety Assessment Model \(SSAM\) can automatically estimate traffic conflicts from simulated trajectories across widely used platforms such as VISSIM, AIMSUN, and PARAMICS \(Gettman et al., 2008\). The significant correlation between simulated conflicts and actual crash data underscores the validity of microsimulation models for safety evaluations. 

However, certain challenges persist in using microsimulation models \(Saunier & Sayed, 2007; Tarko & Songchitruksa, 2005; Xin et al., 2008\). One major concern is the sensitivity of these models to calibration parameters; even slight adjustments can significantly alter the results. 

Additionally, these models often assume that road users follow strict rules to avoid collisions, which may not accurately reflect real-world behavior. More specifically, evasive actions and the accepted distances between road users are particularly challenging to replicate in simulations. To address these challenges, researchers have explored methodologies to enhance the reliability of simulated conflicts. Cunto & Saccomanno \(2008\) developed a four-step calibration framework involving heuristic selection, statistical screening, factorial analysis, and genetic algorithms to 18 





match simulated conflicts to field-measured data. Their approach, validated using crash potential indices, showed that simulated outputs can reliably represent observed traffic patterns within a 95% confidence interval. Similarly, Fan et al. \(2013\) proposed a two-step calibration procedure for freeway merge areas, significantly reducing errors and achieving consistency between simulated and field-observed conflicts. Huang et al. \(2013\) extended this methodology to intersections but noted limitations in capturing conflicts resulting from illegal driving maneuvers, such as unauthorized lane changes. 

Archer \(2005\) explored the use of VISSIM microsimulation modelling for safety assessment at a T-junction. It highlighted the limitations and potential of this approach, particularly in gap-acceptance behaviour. The study introduced a probabilistic gap-acceptance function, ** **addressing the shortcomings of the conventional fixed critical-threshold approach. An accurate calibration of the** **car-following model** **was essential to realistically capture time-gap distributions**. **While the simulation tended to underestimate serious conflicts, it proved to be a valuable tool for safety assessment. Essa & Sayed \(2015a\) explored rear-end conflicts using VISSIM and PARAMICS, proposing a two-step calibration process to march field conditions and optimize parameters using genetic algorithms. While this method improved the correlation between simulated and field conflicts, discrepancies in spatial conflict distributions and exposure levels were observed. 

Moreover, PARAMICS tended to overestimate conflicts at lower TTC thresholds, while VISSIM 

showed the opposite trend. Further research by Essa & Sayed \(2015b\) on parameter transferability revealed that calibration could be expedited across different intersections, although some parameters, such as following thresholds, required case-specific adjustments. 

Similarly, Y. Guo et al. \(2019\) further highlighted the importance of matching field and 19 





simulation conditions to enhance reliability, emphasizing that the direct transfer of traffic parameters across environments with differing regulations might lead to erroneous safety assessment. ** **

In recent studies, the implementation of Automated Vehicles \(AVs\) in traffic flow has raised new concerns regarding safety assessments in mixed traffic conditions composed of both traditional vehicles and AVs. Given the lack of real-world crash data for AVs, research suggests that surrogate safety measures, such as traffic conflicts, are essential for evaluating safety in AV 

environments \(Coropulis et al., 2024\). To address this, they tested the suitability of the Gipps model for simulating AVs on a two-way, two-lane rural road network. The analysis identified key parameters, such as clearance and safety margin factors, that significantly influence safety performance in these mixed traffic conditions. The findings offer valuable insights into traffic model calibration for AV scenarios. 

Beyond AV integration, researchers have examined the broader challenges of using microsimulation models for traffic safety evaluation, particularly in non-lane-based heterogeneous traffic environments that are common in developing countries \(Mahmud et al., 2019\). While microsimulation models have advanced in safety assessments, gaps remain in accurately representing driver behavior, especially in these complex environments. 

Heterogeneous traffic conditions demand models capable of capturing more diverse vehicle interactions and road usage patterns, which are often overlooked in traditional lane-based simulations. Addressing these gaps is crucial for improving the reliability and applicability of microsimulation models in diverse traffic settings. Therefore, despite their promising results for 20 





safety assessments, microsimulation models have limited ability to accurately reproduce road users' behavior, particularly under illegal or unexpected maneuvers. 

Expanding microsimulation models to address other road user types also deserves attention. For example, pedestrian-vehicle interactions have been investigated using agent-based models, such as Waizman et al. \(2015\) which incorporate real and simulated data to analyze risk indicators like TTC and braking rate. These models utilize advanced techniques, such as graph-based calculations, to assess relative distances and speed differences between pedestrians and vehicles, and they provide valuable insights into dynamic interactions under high-risk conditions. Hacohen et al. \(2018\) similarly created an agent-based simulation system to model pedestrian-vehicle interactions at crossings using a Probabilistic Navigation Function \(PNF\). 

**2.3 Pedestrian Traffic Simulation Models **

Early studies on pedestrian movement relied on the based principles of pedestrian flow, including speed, density, and preferred distance to obstacles. Chattaraj et al. \(2009\) examined pedestrian flow attributes in German and Indian cultures, finding that Germans require more personal space and that corridor length had no impact on movement. Ye et al. \(2008\) analyzed flow-density-speed relationships in various facilities, discovering that passageways have higher capacities than stairways and that two-way passageways lead to lower speeds due to increased conflict occurrence. Also, Discrete Choice Models \(DCMs\) can simulate pedestrian decision-making by analyzing variables like distance, speed, and TTC. Cheng et al. \(2014\) introduced metrics like the Pedestrian Safety Conflict Index \(SCI\) to assess safety, while Pascucci et al. 

\(2017\) explored pedestrian conflicts but faced challenges in capturing nuanced behaviors like courtesy and generalizability across contexts. Antonini et al. \(2004, 2006\) simulated 21 





homogeneous pedestrian environments but noted limitations in applying their models to mixed-road conditions. 

Over the years, microsimulation models like Cellular Automata \(CA\) and Social Force Models \(SFM\) have been developed for human motion prediction, primarily focusing on path planning and obstacle avoidance, but lacking traffic safety assessment. The SFM was introduced by Helbing and Molnár \(1995\) and models pedestrian behavior through external forces and personal motivations. It has been applied to evacuation scenarios \(Helbing et al., 2000\) and expanded to include desired, social, and granular forces for predicting evacuation times \(Parisi & Dorso, 2005\). Zeng et al. \(2014\) used SFM to simulate pedestrian crossings at signalized intersections, while Z. Zhou et al. \(2019\) studied its application during the Pedestrian Flashing Green phase. 

Refinements include psychosocial dynamics \(Karamouzas et al., 2009\) and group behavior modeling \(Farina et al., 2017\), and Moussaïd et al. \(2010\) explored crowd spatial patterns across different densities. Alternatively, CA models provide grid-based frameworks for simulating pedestrian interactions. Burstedde et al. \(2001\) applied a floor field model to evacuation scenarios, while Xie et al. \(2012\) used a CA approach to categorize pedestrian behaviors and analyze safety measures at signalized intersections, showcasing CA’s versatility in exploring pedestrian dynamics. R.-Y. Guo \(2014\) enhanced CA with finer spatial discretization to simulate multi-cell pedestrian movements. T. Liu et al. \(2020\) integrated fuzzy logic with CA to optimize exit usage in evacuations, while Lu et al. \(2016\) calibrated CA for pedestrian-vehicle interactions at unsignalized crosswalks. 

Furthermore, Agent-Based Models \(ABMs\) may address the complexity of mixed traffic settings by simulating interactions among autonomous agents. Studies by Erol et al. \(1998\), Jennings 22 





\(2000\), and Macal & North \(2005\) highlight ABM's ability to model intricate behaviors and adapt to varying conditions. ABM operates as a bottom-up approach, enabling detailed analysis of micro-level interactions and their aggregate effects on transportation systems. Its flexibility makes it well-suited for dynamic environments, providing insights into safety measures and traffic management strategies. Rad et al. \(2020\) utilized ABM simulation implemented in AnyLogic software to investigate pedestrians' decision-making processes in the presence of AVs. 

Factors such as distance from approaching vehicles, age, familiarity with AVs, and communication between AVs and pedestrians were found to significantly influence crossing behaviors. Interestingly, gender did not show a significant impact on pedestrians' decision-making. 

More advanced frameworks, such as Markov Decision Processes \(MDP\) and Inverse Reinforcement Learning \(IRL\), which provide more sophisticated methods for modeling pedestrian behavior and decision-making, will be explored in detail in the following subsections. 

**2.3.1 Markov Decision Process **

Previous studies often relied on predefined rules to govern the behavior of agents within simulation environments, with adjustments to these rules representing the primary avenue for enhancing simulation accuracy. However, a novel alternative to traditional rule-based approaches involves integrating intelligence into agents' decision-making processes. The Markov Decision Process \(MDP\) framework offers a mathematical methodology that enables agents to learn from experience and optimize their behaviors based on observed outcomes. This approach has been successfully applied in various studies to simulate both pedestrian and vehicle behaviors, showcasing its adaptability and effectiveness in complex urban environments. 

23 





For instance, Hsu et al. \(2018\) utilized an MDP framework to model pedestrian-vehicle interactions at unsignalized intersections. In their approach, MDP states were defined by factors such as pedestrian distance from the intersection, pedestrian speed towards the intersection, and vehicle proximity to the intersection. A carefully designed a utility function that penalized vehicles for entering crosswalk areas simultaneously with pedestrians, thereby encouraging safer interactions between pedestrians and vehicles. Similarly, Brechtel et al. \(2011\) combined MDP 

with Dynamic Bayesian Networks \(DBN\) to formulate optimal driving strategies. Their study aimed to derive drivers' optimal decisions in complex traffic scenarios, defining a utility function that incentivized drivers to achieve multiple goals, including driving at maximum speed without collisions, adhering to traffic regulations, and ensuring economical and comfortable driving practices. The model performance evaluation involved simulating driver behaviors in scenarios such as a two-lane highway, demonstrating the efficacy of MDP in capturing decision-making processes and optimizing traffic flow dynamics. 

**2.3.2 Inverse Reinforcement Learning **

In an MDP framework, agents are conceptualized as rational entities making decisions through actions prioritized by a strategy or policy. This policy is informed by environmental cues and interactions with other agents. As agents navigate different environmental conditions, they choose actions that lead to favorable future states. The attractiveness of these states is quantified by reward functions, which not only reflect agent preferences but also guide decision-making in unfamiliar scenarios. Designing effective reward functions for road users poses challenges, typically approached through two main methods. Supervised learning algorithms are used to 24 





mimic desired behaviors through manually crafted rewards, though these can inadvertently promote unintended actions \(Amodei et al., 2016\). 



Alternatively, Inverse Reinforcement Learning \(IRL\) learns reward functions from observed human behaviors \(Ng & Russell, 2000\), a method increasingly applied in recent studies. For instance, Martinez-Gil et al. \(2020\) employed an IRL algorithm based on maximum causal entropy to simulate pedestrian navigation. Pedestrians could adjust speed and direction across multiple intensity levels to reach a specified goal amid obstacles. State features like distance to target, obstacle proximity, speed, and angles were critical in defining agent behaviors. 



In recent research by Alsaleh & Sayed \(2020\), two distinct Inverse Reinforcement Learning \(IRL\) algorithms, namely Feature Matching and Maximum Entropy, were utilized to model cyclist behavior in shared environments. Their findings underscored the effectiveness of the Maximum Entropy IRL algorithm in accurately replicating real cyclist trajectories. Building on this, another study \(Alsaleh & Sayed, 2021b\) explored the application of linear and nonlinear reward structures to analyze cyclist interactions with pedestrians. This research introduced a simulation framework employing Deep Reinforcement Learning \(DRL\) to optimize decision-making policies. Comparisons revealed that the Gaussian Process reward function captured the heterogeneous nature of cyclist behavior more effectively than linear reinforcement learning methods. 

25 





**2.3.3 Multi-Agent Adversarial Inverse Reinforcement Learning** This method utilizes deep neural network discriminators to model road user reward functions, enabling the representation of continuous, complex, and nonlinear reward structures. 

Additionally, road user policies are modeled using deep neural network generators, which can capture intricate and nonlinear behaviors. Calculating the partition function is feasible only for small-scale problems, limiting the applicability of MaxEnt to complex scenarios with high-dimensional spaces and uncertain dynamics. As an alternative, Adversarial Inverse Reinforcement Learning \(AIRL\) was proposed to address larger-scale challenges \(Fu et al., 2017\). This method builds upon Guided Cost Learning \(GCL\) and employs generative adversarial networks \(Finn et al., 2016\). The generative network aims to model authentic distributions effectively, maximizing the likelihood of fooling the discriminator. The MA-AIRL 

framework was introduced to recover reward functions correlating with real-world values, further enhancing its practical application in modeling multi-agent interactions \(Yu et al., 2019\). 



In a related advancement, Alsaleh & Sayed \(2021a\) extended their work using the Multi-Agent Adversarial Inverse Reinforcement Learning \(MA-AIRL\) algorithm to develop a sophisticated simulation framework for pedestrian-cyclist interactions. This framework incorporated a multiagent Actor-Critic Deep Reinforcement Learning \(DRL\) approach to simulate and predict complex interaction dynamics, significantly improving trajectory prediction compared to previous Gaussian Process Inverse Reinforcement Learning methods. This study demonstrated the efficacy of MA-AIRL in enhancing accuracy and realism in modeling multi-agent behaviors in dynamic environments, especially in mixed traffic spaces. 



26 





Building on this, Alsaleh & Sayed \(2021a\) implemented the MA-AIRL approach to simulate pedestrian-cyclist conflicts in shared spaces, using a multi-agent game \(MG\) to concurrently simulate road user decisions. This method, unlike traditional time-step payoffs seen in game-theoretic models, incorporated the Logistic Stochastic Best Response Equilibrium \(LSBRE\) solution to handle agents with bounded rationality. Results showed MA-AIRL outperformed baseline models, accurately predicting road user behavior and evasion techniques. Nasernejad et al. \(2021a, 2023\) expanded on their previous work by addressing the limitations of single-agent frameworks in pedestrian-vehicle conflict modeling, proposing a multi-agent simulation framework based on MG and MA-AIRL to model pedestrian-vehicle interactions in mixed traffic environments. 



While these advancements show promising results, challenges remain in accurately modeling pedestrian behaviors in complex, mixed environments, especially distracted pedestrian-vehicle interactions. These dynamics, often oversimplified in current models, influence conflict occurrence and severity. This study addresses these challenges by focusing on pedestrian behavior during prohibited signal phases and using MA-AIRL to simulate vehicle-pedestrian interactions with greater realism. The MA-AIRL approach contributes by modeling diverse pedestrian behaviors, which can be integrated into advanced technologies to better account for unpredictable pedestrian actions. 

**2.4 Jaywalking Behavior and Interactions **

Previous jaywalking studies have primarily explored the factors associated with jaywalking and its safety hazards. Human factors significantly affect pedestrians’ crossing behavior, often 27 





leading them to cross illegally instead of using designated facilities. For example, Li et al. \(2014\) identified predictors of pedestrians’ intentions to jaywalk, such as past behavior, situational factors \(e.g., high-time pressure, descriptive norms, and being unsupervised\), and reliance on habitual rather than deliberate decision-making. In this case, "unsupervised" refers to the absence of others who might influence behavior through social facilitation. Additionally, under time pressure, it was observed that individuals often filter information and accelerate decision-making, relying on habits rather than detailed cognitive evaluations. Other factors include socioeconomic conditions, gender, age, traffic conditions, and urban infrastructure. For instance, Vasudevan et al. \(2022\) examined how low-income pedestrians interact with vehicles and found that financial constraints both limit their transportation choices and increase their reliance on unsafe road crossing. Additional studies found that male pedestrians are more inclined to jaywalk when compared to females, and this behavior is also influenced by mobile phone use, clothing type, and pedestrian volume \(Anik et al., 2021; Tiwari et al., 2007\). Young males generally have more positive attitudes towards violations, perceive fewer inhibitory norms \(feel less constrained by social or moral rules\), and report violations more frequently than elderly people and women \(Moyano Dı́az, 2002\). Moreover, Guo et al. \(2012\) found that pedestrians often act based on personal characteristics rather than the environment, and this might explain why some people commit traffic violations despite knowing the associated risks. 

Other studies indicate that jaywalking is significantly influenced by signal timing, traffic speed, volume, number of lanes, crosswalk width, and physical barriers. Longer waiting times and increased crossing distances tend to increase the likelihood of jaywalking \(Bansal et al., 2022; H. 

Guo et al., 2012\). Li \(2013\) modeled pedestrians' intended waiting times at signalized 28 





intersections and discovered that most pedestrians tend to either cross the street immediately after arriving at the crossing point or wait for the entire duration of the red phase before crossing. 

This indicates that a large proportion of pedestrians exhibit extreme behaviors: either they are impatient and cross right away, or they are more patient and wait for the light to change. 

Sisiopiku and Akin \(2003\) observed that, in signalized intersections, low vehicle traffic demand is a key component in evaluating pedestrians’ compliance with signal timings. Therefore, the design and location of pedestrian facilities play a crucial role in encouraging pedestrians to safely cross at crosswalks. Furthermore, the decision to use a crosswalk is highly dependent on its proximity to a pedestrian's desired destination. Ansariyar and Jeihani \(2023\) found that increased jaywalking frequencies and faster jaywalking speeds lead to more frequent and severe vehicle-pedestrian conflicts. They also noted that adverse weather, like cloudy and rainy days, motivates pedestrians to jaywalk more. Also, Bella and Nobili \(2020\) observed that jaywalking makes drivers delay braking and execute more abrupt maneuvers, resulting in lower minimum speeds and higher deceleration rates. Additionally, XIE et al. \(2017\) and Russo et al. \(2018\) found that jaywalking tendencies increase as pedestrian flow increases and as vehicle flow decreases. This is likely because, in areas with heavy pedestrian flow and fewer vehicles, pedestrians may feel safer or more willing to cross the street despite the traffic signals. With fewer vehicles on the road, there might be greater gaps between vehicles, which can increase the frequency of jaywalking. 

To better understand and predict jaywalking behavior, researchers have employed various modeling techniques. Artificial Neural Networks \(ANNs\), for example, have been used to model pedestrian gap acceptance behavior, which supports understanding their decision-making process 29 





during jaywalking \(Raghuram Kadali et al., 2014\). Other models, such as Multi-Linear Regression \(MALR\) and Structural Equation Modeling \(SEM\), have also been applied to analyze the effects of various factors on jaywalking behavior and to predict their intentions to jaywalk \(Aden et al., 2020; Hamidun et al., 2021\). More recently, Agent-based Modeling \(ABM\) emerged as a promising approach for simulating pedestrian behavior as it assumes that road users are agents that make strategic decisions within an environment. Hussein and Sayed \(2019\) validated an agent-based pedestrian microsimulation model in real-world scenarios, but did not capture jaywalking behavior within their modeling framework. Zhu et al. \(2021\) applied ABM to predict pedestrian crosswalk behavior; however, complex pedestrian paths and group movements still deserved further exploration. MDPs are also essential for modeling road user behavior as agents seek to maximize their expected cumulative rewards \(i.e., their utilities over time\), which makes them suitable for dynamic road environments as shown by several previous studies \(Alsaleh & Sayed, 2020; Nasernejad et al., 2021a\). However, MDPs typically assume single-agent scenarios, which limits their effectiveness in complex traffic situations. Alternatively, MGs offer a solution by incorporating a multiagent framework, where multiple agents are captured considering an equilibrium structure. This provides a more realistic representation and better accounts for road user preferences and responses \(Alsaleh & Sayed, 2021a; Nasernejad et al., 2023\). 

Recent advancements in Autonomous Vehicle \(AV\) technologies have introduced new dimensions to pedestrian-vehicle interaction studies, especially in complex scenarios like jaywalking. Researchers have developed sensor-based systems, such as utilizing LiDAR 

technology, to monitor pedestrian behaviors at signalized intersections. Taylor Li et al. \(2023\) 30 





discussed the critical role of smart transportation systems in addressing pedestrian safety, concluding that current signal designs and detection technologies are often biased toward vehicle design. This bias can result in longer pedestrian delays and insufficient walk times, which may encourage risky behaviors such as jaywalking. Vasudevan et al. \(2022\) explored pedestrian-vehicle interactions on midblock crossings using LiDAR data. Ansariyar and Jeihani \(2023\) utilized LiDAR sensors to monitor jaywalking behaviors at signalized intersections, classifying key factors that influence the jaywalking frequency and its impact on vehicle-pedestrian conflicts. These studies show the potential for AVs to adapt to jaywalking through improved detection and interaction mechanisms. Additionally, there is a growing interest in forecasting pedestrian actions for advanced AV traffic management systems. Recent advancements indicate that techniques such as DRL will play a major role in enhancing the predictive capabilities of AVs \(El Hamdani et al., 2021\). DRL techniques enable more accurate predictions of pedestrian behavior by learning complex patterns from large datasets. This has the potential to improve AVs' abilities to anticipate and respond to pedestrian movements, leading to safer traffic systems. 

The existing research on jaywalking behavior and pedestrian-vehicle interactions highlights the need for advanced modeling techniques to address the safety risks associated with jaywalking. 

While previous studies have explored pedestrian and vehicle behaviors, most approaches lack a framework that simultaneously considers the intentions of both road users in increased-risk situations such as jaywalking. Unlike traditional models, MAAIRL can capture the bidirectional dynamics of pedestrian-vehicle interactions and their complex decision-making processes, such as a pedestrian’s urgency to clear a conflict point or a driver’s need to avoid a crash. Therefore, this study offers a new perspective on analyzing jaywalking behavior at signalized intersections. 

31 





## Chapter 3: Methodology 

An automated video analysis process was used to extract road user trajectory data from an urban intersection in Vancouver, Canada. Conflicts between pedestrians and vehicles were identified and classified based on jaywalking behavior. From these trajectories, micro-level behavioral parameters such as speeds and accelerations were calculated. Then, this study employed MAAIRL to model the interactions between pedestrians and drivers by treating road users as rational and intelligent agents. Two separate models were developed: a non-jaywalking pedestrian-vehicle model and a jaywalking pedestrian-vehicle model. In this framework, MGs were utilized to represent the road users into states and actions, Adversarial Inverse Reinforcement Learning \(AIRL\) was used to recover the reward functions, and Multiagent Actor-Critic Deep Reinforcement Learning \(MAAC-DRL\) was considered to derive the optimal policies. More specifically, the Multiagent Actor-Critic Deep Reinforcement Learning with Kronecker factors \(MACK\) approach was employed to optimize the policies of the agents in this study. This process is illustrated in Figure 3.1. 

32 





CLASSIFICATION

\(sampled distributions vs. 

actual behaviour\)

VIDEO DATA

ROAD USER

TRAINING DATASET

DISCRIMINATOR

TRAJECTORIES

Agent 1: Pedestrians

Agent 2: Vehicles

Agent 1: Pedestrians

Agent 1: Pedestrians

REWARD FUNCTION

Agent 2: Vehicles

Agent 2: Vehicles

Agent 1: Pedestrians

Agent 2: Vehicles

MULTI-AGENT ACTOR-CRITIC DRL \(MACK\)

*ACTIONS*

Agent 1: Pedestrians

*STATES*

*ERROR*

*REWARDS*

CRITIC

ACTOR

*ERROR*

TESTING DATASET

ENVIRONMENT

Agent 1: Pedestrians

Agent 2: Vehicles

Agent 2: Vehicles

*STATES*

*ERROR*

*POLICY*

CRITIC

ACTOR

*REWARDS*

*ERROR*

*ACTIONS*

GENERATOR

*SIMULATED ROAD USER TRAJECTORIES*

Agent 1: Pedestrians

Agent 2: Vehicles



**Figure 3.1 Pedestrian-Vehicle Interactions Modeling Framework** **3.1 Study Site **

The location under study is the East Hastings & Main Street intersection, which is located on the east side of Downtown Vancouver. This intersection features a high pedestrian volume on all four approaches, with notable pedestrian jaywalking behavior. The area surrounding the intersection offers a wide range of commercial services and amenities that attract various demographics. The intersection has a high conflict rate between crossing pedestrians and turning vehicles, and vehicle flow is often disrupted by pedestrian violations. 

33 





Data was collected from 9 am to 5 pm on December 6, December 7, and December 12, 2011, for Scenes 1, 2, and 3, respectively, as indicated in Figure 3.2. Scene 1 focused on the east area of the intersection, facing south. It captured eastbound through and northbound right-turning vehicle volumes, as well as conflicts \(1\) between northbound right-turn vehicles and east-west crossing pedestrians and \(2\) between eastbound through vehicles and north-south crossing pedestrians. Scene 2 pointed south to cover the southwest portion of the intersection. It recorded \(1\) pedestrian crossings with southbound traffic at the southern crossing along East Hastings and \(2\) conflicts between north-south pedestrians on the western crossing of Main Street with eastbound traffic volume. Finally, Scene 3 was a complement of Camera 2. It covered the remaining portion of the pedestrian western crossing on Main Street and the western part of the northern pedestrian crossing along East Hastings. 





**Figure 3.2 Site Location: East Hastings Street & Main Street Intersection** 34 





**3.2 Automated Road Safety Analysis **

Numerous developments in computer vision \(CV\) have greatly enhanced the capabilities to detect traffic conflicts, which have significantly improved the accuracy and efficiency of safety evaluations. This study uses CV to detect and track road users in urban intersections, and the trajectory data extracted from this process was used to identify traffic conflicts, as shown in Figure 3.3. This automated approach has been validated in several previous studies \(Saunier and Sayed, 2007; Sayed et al., 2013; Zaki et al., 2012\). 



**Figure 3.3 Automated Conflict Analysis **

**3.2.1 Camera Calibration **

The first step involves camera calibration, which is a transformation to map two-dimensional coordinates from the video camera into a three-dimensional real-world space. This process considers various properties related to the camera and its lens, including extrinsic parameters \(e.g., camera position and orientation\) and intrinsic parameters \(e.g., focal length, skew angle, and radial lens distortion\). Features were annotated on the background image and corresponding features in an aerial orthographic photo of the intersection. Four types of annotations were used: \(1\) Corresponding Points, \(2\) Distances, \(3\) Angles, and \(4\) Global Up Directions. The 35 





differences between these features in both the background image and the aerial orthographic photo resulted in an objective function being minimized, which leads to a homography matrix \(Ismail et al., 2013\). 

**3.2.2 Road user Detection and Tracking **

To detect and track road users, the advanced algorithms YOLOv8 for detection and BoTSORT 

for tracking were utilized \(Jin, 2024; T. Li, Li, et al., 2023\). These algorithms enable identifying and tracking various road users, including vehicles and pedestrians. YOLOv8 classifies road users into categories and provides information on detection frames, positions, and bounding box dimensions, which are crucial for calculating motion variables like speed and acceleration. 

BoTSORT provides tracking capabilities using advanced data association methods. These methods combine motion models, which predict the objects’ trajectories based on their previous positions, with appearance models \(i.e., using visual features to distinguish between objects\). 

This approach ensures accurate tracking even in scenarios with occlusions or dense traffic. In this process, raw images retain unprocessed scene information, which offer more detail compared to pre-processed images commonly used in conventional object detection systems. 

This reduction in pre-processing steps lowers the computational and enhances both detection accuracy and speed. This is crucial for real-time traffic monitoring and analysis. Finally, the algorithm integrates motion and appearance models to handle occlusions and crowded environments effectively, ensuring accurate and stable tracking of road users across frames. 



It should be noted that the YOLO model for object detection was trained through a series of steps. First, different frames were extracted from the raw videos. For each video, a random 36 





selection of 150 images and 100 consecutive frames was extracted, ensuring flexibility in frame selection while targeting a total sample size of 5,000 to 20,000 frames. Although object detection studies typically use larger datasets to enhance model generalization and accuracy, this range was selected as a practical balance, given that a single intersection may not necessitate as much variation in object movements \(Geiger et al., 2012; Tang et al., 2024\). Images were then annotated using the MakeSense.ai tool, where labels were created for different road user types and exported as YOLO-format text files \(Md. R. Islam & Horio, 2024\). A directory structure for training was then established, splitting data into 80% for training and 20% for validation \(C. Liu et al., 2018\). This process allowed for enhanced object detection and road user tracking at the intersection. 

**3.2.3 Conflict Detection **

This research uses both the Time-to-Collision \(TTC\) and the Post-encroachment Time \(PET\) conflict indicators to assess conflict severity. The TTC can be defined as the time until a collision occurs if road users maintain their current paths and speeds, while the PET evaluates the time difference between the first road user leaving the conflict point and the second road user arriving at the same point. To differentiate between regular interactions and conflicts, thresholds of 5 seconds for both TTC and PET were used, as consistent with previous safety studies \(Z. 

Islam et al., 2022; Johnsson et al., 2021\). Additionally, manual validation was conducted on a subset of the events to ensure the accuracy of the conflict extraction procedure. Moreover, the interactions were categorized into two groups: jaywalking pedestrian-vehicle interactions and non-jaywalking pedestrian-vehicle interactions. 

37 





**3.2.4 Data Extraction Results **

The automated video analysis identified a total of 790 pedestrian-vehicle interactions, comprising 382 non-jaywalking pedestrian-vehicle and 408 jaywalking pedestrian-vehicle interactions. On the non-jaywalking subset, 286 interactions were included in the training set and 96 interactions were considered in the test set. For the jaywalking subset, 306 interactions were assigned to the training set, while 102 interactions were used for testing. Jaywalking was defined as crossing when prohibited, which includes pedestrians crossing during a steady hand signal \(indicating “Don’t Walk”\) or during a flashing hand signal \(indicating that it is too late to cross\). 

This aligns with its usage in related studies \(Jason & Liotta, 1982; Lewyn, 2017; Mullen et al., 1990\) and city guidelines \(Committee on Transportation and Infrastructure, 2024; Legal Information Institute, 2021; RSBC, 1996; Toronto, 2021\). 

**3.3 Identifying Behavioral Parameters **

The automated road safety analysis resulted in road user spatial and temporal information at each time frame. For each interaction, the trajectory of a road user is represented as *T* and consists of a series of spatial and velocity coordinates, as illustrated in Equation 1. 

𝑇\(𝑡\) = \{'𝑋\!, 𝑌\!, 𝑉"\!, 𝑉\#\!, … , 𝑋%, 𝑌%, 𝑉"%, 𝑉\#%-\} 



\(1\) 





where the X and Y coordinates represent the road user locations at each time step *i* = 1, …, n, and *Vx* and *Vy * stand for the velocity components. To address potential tracking errors, the Savitzky-Golay algorithm was used. It smooths data by applying a polynomial fitting technique 38 





to local subsets of the data, effectively reducing noise while preserving important features and trends \(Savitzky & Golay, 1964\). 

The trajectories were then used to obtain behavioral parameters, such as speeds, distances, accelerations, and yaw rates. Negative acceleration values are used to represent deceleration, while positive values denote an increase in speed. The speed difference between pedestrians and vehicles \(Δ𝑆&'\(\)\*'\+\) indicates the road user is moving faster, and positive values show that the driver is faster than pedestrians. The yaw rate \(y\) is the rate of change in the steering angle, which is generated by the swerving motion and is calculated from the derivative of the heading direction \(φ\). The lateral \(𝑑,-.\) and longitudinal distances \(𝑑,/%0\) are calculated using the angle \( *θ\)* between the road users’ relative distance and the vehicle velocity vector. Additionally, to understand road users’ intentions of motion, the distance to destination is measured by calculating the difference between the instantaneous X and Y coordinates and the road users’ 

final coordinates. Finally, the interaction angle \(Δφ&'\(\)\*'\+\) is used to measure the road users’ 

relative orientation. The equations that represent the calculation of these parameters are presented as follows. 

𝑆\(𝑡\) = 𝑙1 − 𝑛𝑜𝑟𝑚'𝑉", 𝑉\#- 

\(2\) 



𝐴\(𝑡\) = \+2 



\+. 

\(3\) 



Δ𝑆&'\(\)\*'\+ = 𝑆&'\( − 𝑆\*'\+ 

\(4\) 

39 





𝑑𝜑

𝑦\(𝑡\) = 



𝑑𝑡

\(5\) 



𝑑⃑ ⋅ 𝑣⃑

𝜃 = 𝑐𝑜𝑠\)\! @

G 

DE𝑑⃑ED ⋅ E|𝑣⃑|E

\(6\) 



𝑑,-. = HDE𝑑⃑ED ⋅ 𝑠𝑖𝑛𝜃H 

\(7\) 



𝑑,/%0 = HDE𝑑⃑ED ⋅ 𝑐𝑜𝑠𝜃H 

\(8\) 



Δφ&'\(\)\*'\+ = 𝜑&'\( − 𝜑\*'\+ 

\(9\) 





40 





𝑑

∆𝜑𝑣𝑒ℎ−𝑝𝑒

e cnat

𝑣

s

𝑝𝑒𝑑

i D 

𝛽

l

𝑝𝑒𝑑

a nidutignoL elcihVe 𝛽𝑣𝑒ℎ 𝑑

stance Vector

𝑣

Di

𝑣𝑒ℎ

Vehicle Lateral Distance

****

**Figure 3.4 Road users' lateral distance, longitudinal distance, interaction angle, and heading angle** **3.4 Multiagent Modelling **

This study adopts the MAAIRL framework to capture the complexities of road user interactions in traffic environments. While traditional traffic microsimulation studies employing MDP-based Inverse Reinforcement Learning \(IRL\) models have demonstrated effectiveness for modeling the behavior of single agents \(Anvari et al., 2015; Dias et al., 2018; Lin et al., 2014; Nasernejad et al., 2021a\), they often fall short in accurately reflecting the dynamics of multiple interacting agents, such as pedestrians and vehicles, in real-world traffic scenarios. In urban settings, pedestrian decision-making is influenced by various external factors, including the actions of other pedestrians, approaching vehicles, and environmental conditions. Traditional IRL models that treat each agent in isolation tend to oversimplify these interactions. Instead, MAAIRL 

enables simulating multiagent traffic environments by considering pedestrians and vehicles as 41 





rational agents with distinct states and actions \(e.g., speed, proximity, and decision-making under uncertainty\). 

In this study, road users are modeled within an MG, where each agent behaves according to specific goals and strategies. The MAAIRL framework is applied to learn the underlying reward functions that govern the agents' behaviors, effectively capturing their decision-making processes. Subsequently, the MACK algorithm is used to obtain the optimal policies that dictate how agents should act depending on the traffic situation. This approach allows for a more realistic simulation of multiagent interactions, where road users' actions are informed by their goals as well as the behavior of surrounding agents. 

**3.4.1 Markov Games \(MGs\) Concept **

The MG framework extends the traditional MDP approach to model the sequential decision-making of multiple interacting agents \(Nowe et al., 2012\). This approach considers a multiagent context where agents not only act based on their current states but also anticipate the actions and decisions of other agents. An MG is defined by a tuple \(𝑁, 𝑆, 𝐴, 𝑃, 𝜂, 𝑟, 𝛾\) where: 

• 𝑁 is the number of agents, 

• 𝑆 is the set of possible states, 

• 𝐴 = \{𝐴 5

3\}34\! is the set of action spaces for each agent *i*, 

• 𝑃: 𝑆 𝑥 𝐴\! 𝑥 . . . 𝑥 𝐴5 → 𝑃\(𝑆\) is the state transition function, which describes the stochastic transitions between states based on the current state and the actions of all agents, 

• 𝜂 𝜖 𝑃\(𝑆\) → \[0,1\] is the initial state distribution function, 42 





• 𝑟3 ∶ 𝑆 𝑥 𝐴\! 𝑥 . . . 𝑥 𝐴5 → ℝ is the reward function for each agent *i*, 

• 𝛾 𝜖 \[0,1\] is the discount factor that determines the influence of future rewards on current decision-making. 

Each agent’s goal is to maximize its expected return, defined as the sum of discounted rewards over time. Therefore, the objective of an agent is to optimize its policy 𝜋3 \(𝑎3|𝑠\), as indicated in Equation 10. 

𝐸𝑥𝑝𝑅𝑒𝑡6,𝝅\!" = 𝔼

3

8\#$%:',-\#$%:' \[∑

𝛾,\).𝑟3\(𝑠,, 𝒂, 

,9. 

\)|𝑠., 𝑎., 𝜋\] 

\(10\) 



where the time steps *t* and the discount factor 𝛾 influence the future rewards. 

In multiagent systems, an equilibrium structure is required to account for conflicting or collaborative preferences, and numerous techniques have been applied in this regard. For example, the concept of Nash Equilibrium \(NE\) \(Nowe et al., 2012\) is commonly used to solve MGs, where each agent’s policy represents the best response to the policies of others, and no agent can unilaterally change its policy to achieve better outcomes. However, the NE may not always be optimal, especially in cases of bounded rationality where agents do not always act perfectly. To address this, the Correlated Equilibrium \(CE\) \(Aumann, 1974\) extends NE by allowing agents to coordinate their actions, which results in higher expected rewards. Unlike NE, the CE accounts for dependencies between agents’ actions, leading to more cooperative outcomes where agents anticipate others' responses. Both NE and CE, however, assume that agents always act optimally, which is unrealistic in real-world scenarios involving sub-optimal behaviors. 

43 





To account for these issues, the Logistic Quantal Response Equilibrium \(LQRE\) \(McKelvey & Palfrey, 1995\) introduces stochasticity into the agents’ decision-making. In the LQRE, agents select actions based on probabilistic responses, with better actions more likely to be chosen. This approach accommodates sub-optimal behavior while still prioritizing actions that yield higher expected rewards. Moreover, expanding on the LQRE, the Logistic Stochastic Best Response Equilibrium \(LSBRE\) \(Yu et al., 2019\) uses Gibbs sampling and allows modeling rational joint policies in multiagent systems while still accounting for sub-optimal and bounded rationality behaviors. This enables a more accurate simulation of multiagent traffic environments, where agents’ decisions may not always be optimal but reflect more realistic behavior patterns. In this approach, agents optimize their actions based on the fixed decisions of others. The stochastic policy, denoted by 𝜋3\(𝑎3|𝑠\) reflects the agent's likelihood of choosing action 𝑎3 in state 𝑠, also considers the collective actions 𝑎\)3 of other agents, as presented in Equation 11. 

exp\(𝐸𝑥𝑝𝑅𝑒𝑡6,6\!"\(𝑠

𝜋

3

., 𝑎3, 𝒂\)3\)\)

3\(𝑎3|𝑠\) =



\(11\) 

∑- exp\(𝐸𝑥𝑝𝑅𝑒𝑡6,6\!"\(𝑠

" 

3

., 𝑎3′, 𝒂\)3\)\)



The multiagent approach contains a value function 𝑄3, which is crucial for evaluating the efficiency of an agent's actions. It incorporates an entropy concept to quantify the uncertainty of an agent’s policy. This is expressed mathematically in Equation 12, where 𝑟3 represents the reward and ℋ\(𝜋\) denotes the entropy, which introduces randomness into decision-making. 

44 





𝑄𝝅\#$%:' 

. 

:

3

\(𝑠., 𝑎3 , 𝒂\)3\)

= 𝑟

. 

:

3\(𝑠., 𝑎3 , 𝒂\)3\)

\+ 𝔼

iℋ j𝜋.@\!\(. |𝑠.@\!\)k



8\#$%~<=.>𝑠., 𝒂.? 

3

\(12\) 

\+ 𝔼

l𝑄𝝅\#$\(:'\(𝑠.@\!, 𝒂.@\!\)mn 

𝒂\#$%~𝝅\#$%=.>𝑠.@\!? 

3



In the LSBRE approach, agents aim to maximize rewards jointly. To achieve this objective, Markov chains provide transition probabilities that represent sequential equilibriums in the action space, as shown in Equations 13 and 14. 

𝝅.\(𝑎

. 

\!, … , 𝑎5|𝑠.\) = 𝑃 \(p\{𝑧3 \(𝑠.\) = 𝑎3\} 



3

\(13\) 





𝑧.,\(C@\!\)\(𝑠.\)~𝑃.j𝑎.D𝒂. = 𝒛.,\(C\)\(𝑠.\), 𝑠.k



3

3

3

\)3

\)3

\(14\) 

exp t𝑄𝝅\#$%:' 

. 

.,\(C\)

3

j𝑠., 𝑎3 , 𝒛

\(

\)3

𝑠.\)ku

= 



∑- exp t𝑄𝝅\#$%:' 

. 

.,\(C\)\(

"E

3

j𝑠., 𝑎3 , 𝒛

𝑠.\)ku

\)3



**3.4.2 Maximum Entropy Framework **

To model sub-optimal behavior, the Maximum Entropy Inverse Reinforcement Learning \(MaxEnt IRL\) \(Ziebart et al., 2008\) introduces a probabilistic framework. It maximizes the 45 





reward distribution to account for uncertainty in agents’ decisions, therefore ensuring that the most probable trajectory more appropriately matches the observed behavior. Additionally, IRL 

can be used to infer the reward function of an agent by observing its behavior. Unlike traditional reinforcement learning models, which require a predefined reward function to derive optimal actions, IRL focuses on discovering the underlying utilities driving the observed trajectories. 

Consequently, the Maximum Entropy framework ensures that agents probabilistically choose actions that maximize the expected rewards while incorporating randomness into the reward estimation process, and this allows for a more realistic representation of decision-making. 

Therefore, the probability of an agent choosing a trajectory 𝜏 is proportional to the exponential sum of rewards across the trajectory, as detailed in Equation 15. 

:

:

1

𝑝F\(𝜏\) ∝

exp yz 𝑟

\{ |𝜁\(𝑠\!\) ~ 𝑃\(𝑠.@\!|𝑠., 𝑎.\)• 

\(15\) 

𝑍

F\(𝑠., 𝑎.\)

F

.4\! 

.4\! 

where 𝑤 are the feature weights, 𝜁\(𝑠\!\) represents the initial state distribution, and 𝑍F is the partition function that ensures normalization. 

**3.4.2.1 **

**Adversarial Inverse Reinforcement Learning \(AIRL\) **

To recover the reward function from observed behaviors, AIRL integrates Generative Adversarial Networks \(GANs\) and Guided Cost Learning \(GCL\). In AIRL, the generator learns a reward function from expert behavior and mimics this behavior through a candidate policy. 

Simultaneously, the discriminator distinguishes between expert-generated behavior and artificial samples \(i.e., generated by the generator\), providing feedback to refine the generator's policy. 

The process is iterated until the generator produces expert behavior closely enough that the 46 





discriminator cannot distinguish between the artificially generated samples and the actual behavior, which indicates accurate reward function recovery. The generator and the discriminator are trained concurrently, with the discriminator improving its ability to identify fake samples and the generator refining its reward function. Equation 16 and Equation 18 show how the policy training is maximized. 

5

5

𝔼𝝅 |z log j𝐷F \(𝑠, 𝒂\)k• \+ 𝔼 |z log j1 − 𝐷 \(𝑠, 𝒂\)k• 

" 

𝒒\)

F" 

34\! 

34\! 

\(16\) 



where the discriminator 𝐷F\(𝑠|𝑎\) is formalized as follows: exp\(𝑟 \(𝑠, 𝒂\)\)

𝐷

F" 

F\(𝑠|𝑎\) =



\(17\) 

exp j𝑟F \(𝑠, 𝒂\) \+ 𝑞 \(𝑎

" 

H" 

3|𝑠\)k



Here, 𝐷F\(𝑠|𝑎\) is the discriminator function that estimates the likelihood that a state-action pair \(𝑠, 𝒂\) belongs to the expert. Additionally, the discriminator is parameterized by weights 𝑤3, 𝑟F \(𝑠, 𝒂\) is the reward function, and 𝑞 \(𝑎

" 

H" 

3|𝑠\) represents the action-value function parameterized 

by weights 𝜃3. These weights 𝜃 are determined using the discriminator function: 5

𝔼𝒒 |z log j𝐷 \(𝑠, 𝒂\)k − log j1 − 𝐷 \(𝑠, 𝒂\)k• 

\(18\) 

\)

F" 

F" 

34\! 



Finally, Equation 19 ensures that the reward function 𝑟F,I\(𝑠., 𝑎., 𝑠.@\!\) remains consistent by introducing a shape function to handle potential uncertainties. This function is parameterized by 47 





𝑤 and 𝜑, where 𝑠.and 𝑠.@\! are the states at times 𝑡 and 𝑡 \+ 1, and 𝑎. is the action at time 𝑡. The term 𝑔F\(𝑠., 𝑎.\) represents the reward component and ℎI\(𝑠.\) is the shape function at the current state. 

𝑟F,I\(𝑠., 𝑎., 𝑠.@\!\) = 𝑔F\(𝑠., 𝑎.\) \+ 𝛾ℎI\(𝑠.@\!\) − ℎI\(𝑠.\) 

\(19\) 



**3.4.3 Multiagent Actor-Critic Deep Reinforcement Learning with Kronecker Factors** **\(MACK\) **

The Multiagent Actor-Critic Deep Reinforcement Learning with Kronecker factors \(MACK\) approach is used to optimize the policies of the agents in this study, as previously shown in different multiagent environments \(Song et al., 2018\). An Actor-Critic framework consists of two main components: the Actor and the Critic. The actor component is responsible for estimating the agent’s policy, while the critic component evaluates this policy using a value function to ensure its continuous improvement. More specifically, the critic component calculates the value of the state-action pair considering an advantage function, shown in Equation 20, that measures how much better an action is compared to others. This advantage function is important as it makes the critic component guide the actor component in refining the policy over time. The Kronecker-factored approximation is used to efficiently update the parameters of the actor component through a gradient function, which is calculated using Equation 21. 

48 





C\)\! 

𝐴6"\(𝑠, 𝑎

6"'𝑠

∅" 

.\) = z 𝛾K𝑟'𝑠.@K, 𝒂.@K- \+ 𝛾C𝑉∅" 

.@C, 𝒂\)3,.@C-

K4L

\(20\) 

− 𝑉6"'𝑠

∅" 

., 𝒂\)3,.- 



where \(𝑉6" 

∅ \) represents the baseline value function used by the critic component and the policy 

" 

parameters 𝜃3 for each agent are updated by maximizing the expected cumulative return. 

M

𝔼 |z ∇

6" 

H log 𝜋

\(𝑎

\(𝑠, 𝑎 • 

" 

H" 

.|𝑠.\)𝐴∅" 

.\)

.4L

\(21\) 



In this framework, centralized training with decentralized execution is employed. During training, additional information from other agents' actions and states is incorporated to reduce variance in the learning process. However, during execution, each agent relies only on its own state to make decisions. 

49 





## Chapter 4: Results 

The extracted road user trajectories enabled a comparative analysis of the behavioral parameters considering both non-jaywalking pedestrian-vehicle conflicts and jaywalking pedestrian-vehicle conflicts. Subsequently, two distinct MAAIRL models were developed. The models yielded reward functions that provide valuable insights into road user behavior during conflicts and derived optimal policies that show the best actions based on their current states. These optimal policies made it possible to create two simulation platforms: 1. Behavior Replication Platform: This platform was designed to replicate the behaviors observed in both non-jaywalking pedestrian-vehicle and jaywalking pedestrian-vehicle conflicts. It uses the estimated policies to simulate real-world scenarios from the test dataset, and the goal is to replicate the actual trajectories as closely as possible. 

2. Conflict Modeling Platform: This platform models right-turn pedestrian-vehicle conflicts. 

It helps in understanding the variations in behavior between non-jaywalking and jaywalking pedestrians under the same baseline conditions. 

**4.1 Road User Behavioral Characteristics **

The extracted behavioral variables are summarized in Table 4.1, and their distributions are shown in Figure 4.1, Figure 4.2, and Figure 4.3. T-tests and F-tests were conducted to determine if the distributions of these variables were statistically different when comparing non-jaywalking pedestrian-vehicle conflicts to jaywalking pedestrian-vehicle conflicts. The T-test was used to compare the means of the variables in both conflict types and determine if they were 50 





significantly different from each other. Also, the F-test was used to compare the variances of the variables in the different conflict types. 

**Table 4.1 Behavioral Parameter Statistics: Mean \(Standard Deviation\)** **Non-Jaywalking **

**Jaywalking **

**Pedestrian-Vehicle **

**Pedestrian-Vehicle **

**Variable **

**Conflicts **

**Conflicts **

**Vehicle **

**Pedestrian **

**Vehicle **

**Pedestrian **

3.786 

2.312 

3.725 

2.581 

Speed \(m/s\) 

\(2.852\) 

\(1.090\) 

\(3.142\) 

\(1.061\) 

Acceleration 

0.649 

0.065 

0.498 

0.052\* 

\(m/s2\) 

\(4.590\) 

\(3.114\) 

\(4.606\) 

\(3.059\) 

Longitudinal 

2.456 

-2.173 

2.300 

-2.116 

Distance \(m\) 

\(7.673\) 

\(6.721\) 

\(7.591\) 

\(6.123\) 

Lateral Distance 

5.586 

6.058 

5.332 

6.285 

\(m\) 

\(4.594\) 

\(5.534\) 

\(3.939\) 

\(5.040\) 

Distance to 

14.229 

5.393 

13.346 

5.883 

Destination \(m\) 

\(11.339\) 

\(3.692\) 

\(10.564\) 

\(4.078\) 

0.076 

-0.006 

0.069\* 

-0.007 

Yaw Rate \(rad/s\) 

\(1.889\) 

\(2.401\) 

\(1.889\) 

\(2.283\) 

Speed Difference 

1.474 

1.145 

\(m\) 

\(2.973\) 

\(3.261\) 

Interaction Angle 

-0.111 

-0.246 

\(rad\) 

\(1.439\) 

\(1.464\) 

51 





**Non-Jaywalking **

**Jaywalking **

**Pedestrian-Vehicle **

**Pedestrian-Vehicle **

**Variable **

**Conflicts **

**Conflicts **

**Vehicle **

**Pedestrian **

**Vehicle **

**Pedestrian **

\*Not statistically different at the 95% confidence level with respect to non-jaywalking pedestrian-vehicle conflicts considering the T-test The statistical analysis revealed differences between jaywalking pedestrian-vehicle conflicts and non-jaywalking pedestrian-vehicle conflicts. Vehicles had slightly higher average speeds in non-jaywalking pedestrian-vehicle conflicts, and pedestrians moved faster in jaywalking pedestrian-vehicle conflicts, which aligns with the fact that pedestrians often prioritize speed and efficiency over safety during crossings \(Z.-P. Zhou et al., 2013\). This suggests that behavioral tendencies toward faster movements in jaywalking-related conflicts could be related to perceived urgency or efficiency. Similarly, Li \(2013\) identified abrupt behaviors among pedestrians \(e.g., some pedestrians crossed immediately while others waited for the full signal cycle\). This reflects diverse behavioral patterns that may explain these observed speed differences. 

Cohen's d statistic was also calculated to verify if some differences have practical significance in a real-world context. This metric may be used to overcome limitations in datasets with large sample sizes. The negligible Cohen's d values for variables like acceleration \(Cohen's d = 0.004\) and yaw rate \(Cohen's d = 0.001\) imply that the observed statistical differences could be attributed to sample variability rather than differences in behavior. These findings are consistent with Guo et al. \(2012\), who noted that pedestrians may act based on personal characteristics rather than external traffic conditions. 

52 





Longitudinal and lateral distances between vehicles and pedestrians were slightly smaller in jaywalking pedestrian-vehicle conflicts, which suggests closer interactions and an increase in conflict risk. This is related to previous studies that found that jaywalking frequency and faster jaywalking speeds may lead to more frequent and severe vehicle-pedestrian conflicts \(Ansariyar 

& Jeihani, 2023\). Additionally, Bella and Nobili \(2020\) observed that jaywalking could result in drivers delaying braking and executing abrupt maneuvers. This may contribute to reduced distances between pedestrians and vehicles in jaywalking pedestrian-vehicle conflicts. 

These results show that MAAIRL models may allow for a more comprehensive understanding of how jaywalking pedestrians and vehicles adapt to each other's actions. As these models may capture different representations of behavior, they models can reveal additional insights into how to improve safety measures and inform transportation policies more effectively. Additionally, the MAIRL model can implicitly account for factors like driver behavior, road user equilibrium structure, and pedestrian decision-making processes, which are often overlooked in other approaches. 

20000

15000 20000

15000

Frequency

10000

Frequency

10000

Frequency

5000

Frequency

5000

0

0 0

0

0

1

2

3

4

5

6

−10

−5

0

5

10

0

1

2

3

4

5

6

−10

−5

0

5

10

Pedestrian Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

Pedestrian Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

****

****

25000

20000

15000

15000

Frequency

10000

Frequency Frequency

5000 10000

Frequency

53 

5000

0

0 0

0



−30

−20

−10

0

10

20

30

0

5

10

15

20

25

30

−30

−20

−10

0

10

20

30

0

5

10

15

20

25

30

Pedestrian Longitudinal Distance \(m\)

Pedestrian Lateral Distance \(m\)

Pedestrian Longitudinal Distance \(m\)

Pedestrian Lateral Distance \(m\)

15000

15000

15000

15000

Frequency

Frequency Frequency

Frequency

5000

5000 5000

5000

0

0 0

0

−10

−5

0

5

10

0

5

10

15

20

25

−10

−5

0

5

10

0

5

10

15

20

25

Pedestrian Yaw Rate \(rad/s\)

Pedestrian Distance to Destination \(m\)

Pedestrian Yaw Rate \(rad/s\)

Pedestrian Distance to Destination \(m\)

20000

15000

20000

15000

10000

Frequency

Frequency

Frequency

10000

Frequency

5000

5000

0

0

0

0

0

1

2

3

4

5

6

−10

−5

0

5

10

0

1

2

3

4

5

6

−10

−5

0

5

10



Pedestrian Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

Pedestrian Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

15000

1500025000

25000

20000

15000

15000

20000

Frequency

Frequency Frequency

Frequency

10000

5000

Frequency

5000

Frequency

Frequency

10000

Frequency

10000

5000

5000

0

0

0

00

0

0

0

0

5

10

15

−10

−5

0

5

10

0

5

10

15

−10

−5

0

5

10

−30

−20

−10

0

10

20

30

0

5

10

15

20

25

30

−30

−20

−10

0

10

20

30

0

5

10

15

20

25

30

Pedestrian Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

Pedestrian Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

Pedestrian Longitudinal Distance \(m\)

Pedestrian Lateral Distance \(m\)

Pedestrian Longitudinal Distance \(m\)

****

Pedestrian Lateral Distance \(m\)

****

20000

15000

15000

25000

20000

15000

20000

15000

10000

15000

Frequency

Frequency Frequency

15000

Frequency

15000

150005000

5000

Frequency

10000

Frequency

0

0 0

0

Frequency

5000

Frequency

Frequency

Frequency

10000

Frequency

5000

5000

0

05000

0

1

2

3

4

5

6

5000

−10

0

−5

5

0

10 5

10

15

−10

−5

0

5

10

0

0

0

0

0

Pedestrian Acceleration \(m s2\)

−40

−20

0

20

40

0

5

P 10

edestr

15

20

ian Speed \(m/s\)

25

30

Pedestrian Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

−40

−20

0

20

40

−10

0

5 −5

10

015

20 5

25

1030

0

5

10

15

20

25

−10

−5

0

5

10

0

5

10

15

20

25

Pedestrian Longitudinal Distance \(m\)

Pedestrian Lateral Distance \(m\)

****

P

Pedestr

edestr

ian Yaw Rate \(rad/s\)

ian Longitudinal Distance \(m\)

Pedestr

P ian Distance to Destination \(m\)

Pedestr

edestr ian Yaw Rate \(r

ian Later

ad/s\)

al Distance \(m\)

****

Pedestrian Distance to Destination \(m\)

25000

20000

15000

15000

15000

15000

25000

15000

15000

15000

Frequency

10000

20000

Frequency Frequency

10000

Frequency

15000

5000

5000

Frequency

Frequency

Frequency

Frequency

5000

Frequency

10000

Frequency

05000

0 0

0

5000

5000

Frequency

0

Frequency

0

0

0

0

5000 0

−30

−20

−10

0

10

20

30

5000

0

−405

− 10

20

15

0

2020

25 40 30

0

5

10

15

20

25

30

0

5

10

15

0

5

10

15

−10

−5

0

5

10

0

−10

−5

0

5

10

0

−10

−5

0

5

10

0

5

Pedestr 10

15

20

25

ian Longitudinal Distance \(m\)

30

P Pedestr

edestr ian Lateral Distance \(m\)

ian Longitudinal Distance \(m\)

Pedestrian Lateral Distance \(m\)

Pedestrian Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

Pedestrian Speed \(m/s\)

−10

−

P 5

edestrian Ac 0

celeration \(m 5s2\)

10

0

5

10

15

20

25

30

Pedestrian Yaw Rate \(rad/s\)

Pedestrian Distance to Destination \(m\)

****

****

Pedestrian Yaw Rate \(rad/s\)

Pedestrian Distance to Destination \(m\)

15000

15000

25000

15000

15000 15000

20000

15000

Frequency

Frequency Frequency

Frequency

Frequency 5000

5000

10000

Frequency

5000 5000

Frequency

10000

Frequency

5000

05000

0 0

0

0

0

0

0

−10

−5

0

5

10

0

−10

5 −5

10

0

15

520

25

10

0

5

10

15

20

25

30

−40

−20

0

20

40

0

5

10

15

20

25

30

−40

−20

0

20

40

0

5

10

15

20

25

30

Pedestrian Yaw Rate \(rad/s\)

Pedestr

Pian Distance to Destination \(m\)

edestrian Yaw Rate \(rad/s\)

Pedestrian Distance to Destination \(m\)

Pedestrian Longitudinal Distance \(m\)

****

Pedestrian Lateral Distance \(m\)

****

Pedestrian Longitudinal Distance \(m\)

Pedestrian Lateral Distance \(m\)

**\(a\) Non-Jaywalking Pedestrian-Vehicle Conflicts **

**\(b\) Jaywalking Pedestrian-Vehicle Conflicts **

**Figure 4.1 Pedestrian Behavioral Parameters **

15000

54 

15000

15000

15000



Frequency

Frequency

5000

Frequency

Frequency

5000

5000

5000

0

0

0

0

−10

−5

0

5

10

0

5

10

15

20

25

30

−10

−5

0

5

10

0

5

10

15

20

25

30

Pedestrian Yaw Rate \(rad/s\)

Pedestrian Distance to Destination \(m\)

Pedestrian Yaw Rate \(rad/s\)

Pedestrian Distance to Destination \(m\)



15000 15000

15000 1500015000

15000 15000

Frequency

Frequency

Frequency

5000

Frequency

Frequency

5000

FrequencyFrequency

5000 50005000

Frequency

5000

5000

5000

0

0 0

0

0

00

0

0

5

10

15

−100

−5

5

0

10 5

10

15

−10

−5

0

5

10

0

5

10

15

−10

−5

0

5

10

0

5

10

15

−10

−5

0

5

10

Vehicle Speed \(m/s\)

Pedestrian Acceleration 

V

\(m s2

ehicle Speed \(m/s\)

\)

Vehicle Acceleration \(m s2\)

Vehicle Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

****

Vehicle Speed \(m/s\)

****

Vehicle Acceleration \(m s2\)

15000

15000

15000

15000

20000

20000

10000

10000

20000

20000 10000

10000

Frequency

Frequency

Frequency

5000

5000

Frequency

5000

Frequency

10000

10000 5000

Frequency Frequency

Frequency

4000

Frequency

10000

Frequency

4000

0

Frequency

10000 40000

Frequency

0

0

4000

0

0 0

0

0

0

5

10

15

0

−10

−5

0

5

10

0

5

10

15

−10

−5

0

5

10

0

0

−30

−20

−10

0

10

20

30

0−30

−20 5 −10

100

10 15 20

20

30

0

5

10

15

20

−30

−20

−

V10

0

10

ehicle Speed \(m/s\)

20

30

0

5

Vehicle Acc 10

eleration \(m 15

s2\)

20

Vehicle Speed \(m/s\)

Pedestrian Acceleration \(m s2\)

−30

−20

−10

0

10

20

30

0

5

10

15

20

Vehicle Longitudinal Distance \(m\)

V

V ehicle Lateral Distance \(m\)

ehicle Longitudinal Distance \(m\)

Vehicle Lateral Distance \(m\)

Vehicle Longitudinal Distance \(m\)

****

Vehicle Lateral Distance \(m\)

****

Vehicle Longitudinal Distance \(m\)

Vehicle Lateral Distance \(m\)

25000

20000

20000 10000

10000

25000

15000

25000

15000 25000 15000

15000

Frequency

10000

Frequency Frequency

10000 4000

Frequency Frequency

4000

Frequency

Frequency

Frequency

10000

5000

Frequency

10000

Frequency

0

0010000

Frequency

5000 10000 0

Frequency

5000 0

0

0

0

5000

−30

−20

−10

0

10

20

30

0

0

5

10

15

20

0

−30

−20

−10

0

10

20

30

0

−10

0

−5

010

515

1020

0

0

10

20

30

40

50

60

−10

−5

0

5

10

0

10

20

30

40

50

60

Vehicle Longitudinal Distance \(m\)

−10

−

V 5

ehicle Later 0

5

al Distance \(m\)

10

Vehicle Longitudinal Distance \(m\)

****

0

10

20

30

40

50

60

−10

−5V

V ehicle Ya 0

w Rate \(r

ehicle Later

ad/s\) 5

al Distance \(m\)

10

****

0

10

V

20

30

40

ehicle Distance to Destination \(m\) 50

60

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

15000

15000 15000

15000

25000

25000 15000

15000

Frequency

5000

Frequency Frequency

Frequency

Frequency

Frequency

5000 5000

10000

5000

Frequency

500010000

Frequency

0

0

0

0 0

5000 0

0

5

10

15

20

0

−10

−5

0

5

10

0

−10

−5

0

5

10

0 0

10

520

3010

40

50

15

60 20

−10

−5

0

5

10

Vehicle Speed \(m/s\)

−10

−

P 5

edestrian Ac 0

celeration \(m 5s2\)

10

0

10

20

30

40

50

60

Vehicle Acceleration \(m s2\)

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

Vehicle Speed \(m/s\)

****

****

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

20000

20000

20000

20000

55 

Frequency

10000

Frequency

10000



Frequency

10000

Frequency

10000

0

0 0

0

−40

−20

0

20

40

0

5

10

15

20

25

30

−40

−20

0

20

40

0

5

10

15

20

25

30

Vehicle Longitudinal Distance \(m\)

Vehicle Lateral Distance \(m\)

Vehicle Longitudinal Distance \(m\)

Vehicle Lateral Distance \(m\)

25000

15000 25000

15000

Frequency

Frequency

10000

5000

Frequency

10000

Frequency

0

0

5000

0

0

−10

−5

0

5

10

0

20

40

60

80

−10

−5

0

5

10

0

20

40

60

80

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

15000

15000

15000

15000

Frequency

5000

Frequency

Frequency

Frequency

5000

5000

5000

0

0

0

0

0

5

10

15

20

−10 0

−5 5

0 10

5 15

10 20

−10

−5

0

5

10

Vehicle Speed \(m/s\)

Pedestrian Acceleration 

V

\(m s2

ehicle Speed \(m/s\) \)

Vehicle Acceleration \(m s2\)

20000

20000

20000

20000

Frequency

10000

Frequency

10000

Frequency

10000

Frequency

10000

0

0

0

0

−40

−20

0

20

40

0

− 5

40

10

−20

15 0

20 20 25

30

40

0

5

10

15

20

25

30



Vehicle Longitudinal Distance \(m\)

Vehicle Later

V

al Distance \(m\)

ehicle Longitudinal Distance \(m\)

Vehicle Lateral Distance \(m\)

25000

25000

15000

15000

Frequency

Frequency

Frequency

Frequency

10000

10000

5000

5000

0

0

0

0

−10

−5

0

5

10

0 −10

20 −5

40 0

60 5

80 10

0

20

40

60

80

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

Vehicle Yaw Rate \(rad/s\)

Vehicle Distance to Destination \(m\)

****

****

**\(a\) Non-Jaywalking Pedestrian-Vehicle Conflicts **

**\(b\) Jaywalking Pedestrian-Vehicle Conflicts **

**Figure 4.2 Vehicle Behavioral Parameters **

5000

6000

10000

10000

Frequency

2000

Frequency

Frequency

4000

Frequency

0

20004000

0

0

−5

0

5

10

15

0

−5

0

5

10

15

−10

0

10

20

30

−10

0

10

20

30

Speed Difference \(m/s\)

****

Speed Difference \(m/s\)

Speed Difference \(m/s\)

Speed Difference \(m/s\)

****

4000

4000

4000

2000

4000

Frequency

Frequency

2000

2000

Frequency

0

Frequency

2000

0

0

−4

−2

0

2

4

0

−3

−2

−1

0

1

2

3

−3

−2

Inter

−1

action Angle \(r

0

ad\) 1

2

3

−3

−2

−1

0

1

2

3

Interaction Angle \(rad\)

Interaction Angle \(rad\)

****

Interaction Angle \(rad\)

****

**\(a\) Non- Jaywalking Pedestrian-Vehicle Conflicts **

**\(b\) Jaywalking Pedestrian-Vehicle Conflicts **

**Figure 4.3 Speed Difference and Interaction Angle **

**4.2 Reward Functions **

This study estimated reward functions for vehicle-pedestrian interactions considering both jaywalking pedestrian-vehicle conflicts and non-jaywalking pedestrian-vehicle conflicts. The MAAIRL model provided optimal policies and reward functions, which were automatically 56 





estimated in the training process. The analysis of jaywalking and non-jaywalking pedestrian reward functions, as well as vehicle reward functions, reveals a detailed understanding of how these agents interact at signalized intersections. These reward functions are plotted in Figure 4.4** **

for jaywalking scenarios and Figure 4.5 for non-jaywalking scenarios. In each figure, subfigure \(a\) represents the vehicle reward function, and subfigure \(b\) represents the pedestrian reward function. The plots within each row were plotted utilizing bivariate state features whilst assuming the mean values for the other state variables. Higher rewards imply higher preferences for certain states, and additional behavioral inferences can be made if other values are selected for the state features. 

The reward function, plotted with longitudinal distance and lateral distance in the left plot of the first row, shows that, in non-jaywalking scenarios, pedestrians initially maintain a smaller lateral distance from vehicles but increase this distance as they approach the point of interaction \(i.e., longitudinal distance approaching zero\). This may possibly be attributed to a perceived risk reduction after the vehicle has passed. This aligns with the findings of Guo et al. \(2012\), who reported that pedestrian behavior is influenced by personal risk perception and environmental conditions. However, in jaywalking scenarios, pedestrians often stay close to vehicles during the interaction, and this indicates a preference to minimize crossing time in the roadway regardless of potential exposure to vehicle conflicts. This behavior is consistent with Zhou et al. \(2013\), who found that pedestrians often prioritize efficiency over safety during road crossings, especially in jaywalking scenarios. Additionally, Bansal et al. \(2022\) observed that longer crossing distances tend to increase jaywalking occurrences, as pedestrians are eager to adopt the shortest possible crossing distance, which further emphasizes efficiency over safety. Moreover, 57 





drivers tend to keep larger lateral distances from jaywalking pedestrians, especially after the point of interaction, and this reflects the increased caution drivers exhibit in response to unpredictable pedestrian behavior. 

Furthermore, the reward function, plotted with longitudinal distance and speed in the middle of the first row, reveals distinct patterns considering jaywalking and non-jaywalking behaviors. In non-jaywalking scenarios, pedestrians increase their speed as they approach the conflict point and decelerate afterward. This behavior suggests an increased sense of self-confidence in their safety during the crossing interaction. Also, jaywalking pedestrians seem to exhibit more cautious behavior at moderate speeds when they approach the conflict point. However, they accelerate after the interaction to clear the road quickly and avoid other potential conflicts, which is consistent with the literature on faster speeds during jaywalking interactions \(Ansariyar & Jeihani, 2023\). Additionally, the jaywalking reward function shows higher variability, with sudden variations in speeds near the conflict point. This unpredictability likely reflects an increased awareness related to \(1\) crossing the road quickly and \(2\) the lack of clear right-of-way. Drivers behave similarly in both jaywalking and non-jaywalking scenarios, slowing down before the interaction and speeding up after. However, they exhibit smaller speed increases in jaywalking scenarios, potentially due to the unpredictability of pedestrian behavior, as indicated by Bella and Nobili \(2020\). These differences show that pedestrians try to minimize their crossing time while jaywalking and that vehicles try to cautiously navigate around them. For example, sample data points were taken at the interaction point \(i.e., a longitudinal distance equal to zero\) to measure the rewards at a speed of 7.2 km/hr \(2.0 m/s\) and 15 km/hr \(4.1 m/s\) for pedestrians and drivers, respectively, when compared to stopped vehicles and pedestrians. It was 58 





found that, by comparing these situations, the increase in the pedestrian reward is 30% greater in jaywalking scenarios when compared to non-jaywalking scenarios. This supports that pedestrians often prioritize speed and efficiency over safety when crossing \(Z.-P. Zhou et al., 2013\). Also, the increase in driver reward is 7% higher in jaywalking scenarios, which reflects a greater effort required by drivers to safely maneuver around unpredictable pedestrian behavior. 

The reward function, plotted with longitudinal distance and speed difference in the right plot of the first row, shows that, in non-jaywalking scenarios, drivers typically move faster than pedestrians before the conflict point, but the speed difference reduces as they overtake them, with pedestrians rarely moving faster afterward. However, in jaywalking scenarios, drivers usually move faster at the conflict point and pedestrians may accelerate after it, which results in closer speed differences or situations where pedestrians move faster than drivers. This more erratic pattern of speed differences in jaywalking scenarios indicates additional unpredictability, and this may challenge drivers to respond safely. These findings align with Bella and Nobili \(2020\), who observed that jaywalking increases unpredictability and requires drivers to delay braking and perform abrupt maneuvers. 

The reward function, plotted with longitudinal distance and interaction angle in the left plot of the second row, indicates that pedestrians and drivers tend to approach each other at more perpendicular angles in non-jaywalking scenarios, which suggests more controlled interactions as pedestrians clear the drivers' path. Conversely, in jaywalking scenarios, pedestrians often approach vehicles from unpredictable angles. This reflects their disregard for structured paths like crosswalks. For example, sample data points were taken at the interaction point to estimate the rewards at an angle of 1.5 radians \(approximately 90 degrees\) when compared to an 59 





interaction angle of 0 radians. At this angle, the increases in pedestrian and vehicle rewards are 34% and 22%, respectively, higher in non-jaywalking scenarios when compared to jaywalking scenarios. This suggests that larger \(i.e., more perpendicular\) interaction angles are preferable for non-jaywalking pedestrians, as they promote safer and more organized crossings. In contrast, smaller interaction angles are preferable for jaywalking pedestrians, as they often attempt to minimize crossing time despite the increased risk. Hence, both pedestrians and drivers experience more controlled and predictable interactions when following structured paths like crosswalks. In contrast, jaywalking scenarios, where pedestrians cross at smaller \(i.e., more parallel\) angles, result in reduced rewards for both road users. The unpredictability in jaywalking scenarios may lead to more risky interactions, where both road users have less time and space to react safely. This suggests that jaywalking pedestrians prioritize efficiency over safety and prefer shorter crossing distances \(Bansal et al., 2022; Z.-P. Zhou et al., 2013\), resulting in more unpredictable and hazardous interactions for both pedestrians and drivers. 

In both jaywalking and non-jaywalking scenarios, the reward function, plotted with the lateral distance and speed in the right plot of the second row, shows that pedestrians prefer higher speeds when close to vehicles, but jaywalking pedestrians exhibit sharper and less gradual speed increases due to their need to clear the road as fast as possible \(Alhajyaseen & Iryo-Asano, 2017; Nasernejad et al., 2021b\). The reward function also shows that drivers adjust their speeds accordingly, but their reaction is more pronounced in jaywalking scenarios as they attempt to maintain control while allowing pedestrians to cross safely. This aligns with Nasernejad et al. 

\(2021b\), who highlight that the unpredictability of pedestrian movements in conflict situations can significantly impact drivers' ability to react, further escalating crash risk. 

60 





The estimated reward functions reflect an equilibrium structure between pedestrians and drivers, where their preferences often align or conflict depending on the situation. For example, in non-jaywalking scenarios, both road users tend to adjust their speeds in response to each other in a relatively synchronized manner. For instance, as pedestrians approach the conflict point, they increase their speeds and drivers simultaneously reduce their speeds to navigate the intersection safely. These changes suggest an interdependent dynamic structure where both road users react to each other’s behaviors. Also, jaywalking scenarios also show the effects of these complementary preferences. Pedestrians, motivated by the need to minimize the time in the roadway, often accelerate after the conflict, while drivers, perceiving this increased risk, respond by maintaining a greater distance or decelerating more cautiously. 

61 





**\(a\) Vehicle Reward Function **

62 





**\(b\) Pedestrian Reward Function **

**Figure 4.4 Reward Functions for Jaywalking Pedestrian-Vehicle Interactions** 63 





12.5

10.0

15

Reward

Reward

Reward

10.0

7.5

10

1

1

7.5

1

5.0

0

5

erence \(m/s\)

0

0

5.0

al Distance \(m\)

Speed \(m/s\)

−1

2.5

−1

0

−1

2.5

Later

−2

Speed Diff

0.0

0.0

−5

−10

−5

0

5

10

−20

−10

0

10

20

−10

−5

0

5

10

Longitudinal Distance \(m\)

Longitudinal Distance \(m\)

Longitudinal Distance \(m\)

15

3

ad\)

Reward

Reward

10.0

Reward

2

1

10

1

1

arget \(m\)

7.5

0

0

5.0

0

1

5

action Angle \(r

Speed \(m/s\)

−1

−1

−1

2.5

Inter

Distance to T

0

0

0.0

−10

−5

0

5

10

−20

−10

0

10

20

0.0

2.5

5.0

7.5

10.0

Longitudinal Distance \(m\)

Longitudinal Distance \(m\)

Lateral Distance \(m\)

15

Reward

ad\) 10.0

Reward

Reward

10

2

12

7.5

1

1

1

arget \(m\)

5

erence \(m/s\)

0

8

0

5.0

0

0

action Angle \(r

−1

−1

2.5

4

−1

Speed Diff

Inter

Distance to T

−5

0.0

0.0

2.5

5.0

7.5

10.0

0.0

2.5

5.0

7.5

10.0

0.0

2.5

5.0

7.5

10.0

Lateral Distance \(m\)

Lateral Distance \(m\)

Lateral Distance \(m\)

12.5

3

15

Reward

ad\)

Reward

Reward

10.0

10

1

2

1

1

7.5

erence \(m/s\) 5

0

0

0

5.0

1

action Angle \(r

Speed \(m/s\)

0

−1

−1

−1

2.5

Speed Diff

Inter

−5

0

0.0

0.0

2.5

5.0

7.5

10.0

12.5

0.0

2.5

5.0

7.5

10.0

12.5

4

8

12

Speed \(m/s\)

Speed \(m/s\)

Distance to Target \(m\)

15

15

3

Reward

Reward

ad\)

Reward

10

10

1

1

2

1

5

erence \(m/s\)

5

0

erence \(m/s\)

0

0

1

0

−1

0

−1

action Angle \(r

−1

Speed Diff

Speed Diff

Inter

−5

−5

0

0

1

2

3

4

8

12

4

8

12

Interaction Angle \(rad\)

Distance to Target \(m\)

Distance to Target \(m\)

****

**\(a\) Vehicle Reward Function **

64 





10.0

15

Reward

4

Reward

Reward

7.5

1

10

3

1

1

0

5.0

5

erence \(m/s\)

0

2

0

al Distance \(m\)

−1

Speed \(m/s\)

2.5

−1

1

0

−1

−2

Later

Speed Diff

0.0

0

−5

−10

−5

0

5

10

−20

−10

0

10

20

−10

−5

0

5

10

Longitudinal Distance \(m\)

Longitudinal Distance \(m\)

Longitudinal Distance \(m\)

4

3

ad\)

Reward

Reward

Reward

10

3

1

1

2

arget \(m\)

1

0

0

2

0

5

1

action Angle \(r

−1

Speed \(m/s\)

−1

1

−1

Inter

−2

Distance to T

0

0

0

−10

−5

0

5

10

−20

−10

0

10

20

0.0

2.5

5.0

7.5

10.0

Longitudinal Distance \(m\)

Longitudinal Distance \(m\)

Lateral Distance \(m\)

15

15

3

Reward

ad\)

Reward

Reward

10

1

2

1

1

arget \(m\) 10

5

erence \(m/s\)

0

0

0

1

0

−1

action Angle \(r

−1

5

−1

Speed Diff

Inter

Distance to T

−5

0

0.0

2.5

5.0

7.5

10.0

0.0

2.5

5.0

7.5

10.0

0.0

2.5

5.0

7.5

10.0

Lateral Distance \(m\)

Lateral Distance \(m\)

Lateral Distance \(m\)

4

15

3

Reward

ad\)

Reward

Reward

3

10

1

2

1

1

erence \(m/s\)

2

5

0

0

0

1

Speed \(m/s\)

−1

action Angle \(r

−1

1

−1

0

Speed Diff

Inter

0

0

0

1

2

3

4

0

1

2

3

4

4

8

12

Speed \(m/s\)

Speed \(m/s\)

Distance to Target \(m\)

15

3

Reward

Reward

ad\)

Reward

10

10

1

1

2

1

erence \(m/s\) 5

5

erence \(m/s\)

0

0

0

1

−1

0

−1

action Angle \(r

−1

0

Speed Diff

Speed Diff

Inter

−5

0

0

1

2

3

0

5

10

15

4

8

12

Interaction Angle \(rad\)

Distance to Target \(m\)

Distance to Target \(m\)



**\(b\) Pedestrian Reward Function **

**Figure 4.5 Reward Functions for Non-Jaywalking Pedestrian-Vehicle Interactions** **4.3 Microsimulation Modelling of Actual Behavior **

To evaluate the performance of the MAAIRL models, a multiagent microsimulation tool was developed to obtain simulated pedestrian-vehicle interactions using the estimated optimal 65 





policies. This simulation tool uses real-world trajectory data, more specifically initial positional data, speeds, and heading directions for both pedestrians and vehicles. Additionally, final coordinates are included to specify the road users’ intentions of motion. Once initialized, the simulation tool calculates state features \(e.g., relative distances, speeds, and angles\) based on these initial parameters, and the multiagent policies provide the corresponding actions considering these states. Therefore, the model dynamically updates each road user's state by continuously incorporating the latest actions. The simulation progresses sequentially through each frame until it reaches the previously assigned number of frames, and this iterative approach is conducted for each trajectory within the test dataset. 

**4.3.1 Performance Evaluation **

Table 4.2** **displays the Normalized Root Mean Square Error \(NRMSE\) results for longitudinal distance, lateral distance, pedestrian speed, and vehicle speed. In this study, NRMSE values are used to assess the differences between actual and the MAAIRL simulated trajectories for both pedestrians and vehicles. This measure standardizes the error measure, reducing the sensitivity to small values. Results reveal that the jaywalking pedestrian-vehicle model exhibited greater errors in longitudinal distance and lateral distance, with NRMSE values that were 11.48% and 3.42% 

higher, respectively, compared to the non-jaywalking pedestrian-vehicle model. Conversely, the non-jaywalking pedestrian-vehicle model had NRMSE for pedestrian speed that was approximately 5.18% higher than the jaywalking vehicle-pedestrian model. Also, the vehicle speed NRMSE for the non-jaywalking pedestrian-vehicle model was about 5.55% lower. 

Additionally, T-tests were conducted to evaluate the statistical significance of these differences, 66 





and results indicate that the differences between both models were not statistically significant. 

Thus, there were no significant discrepancies in the accuracy of both models. 

**Table 4.2 Normalized Root Mean Square Error \(NRMSE\) Values** **Pedestrian-Vehicle **

**Lateral **

**Longitudinal Distance **

**Pedestrian Speed **

**Vehicle Speed **

**Interaction Type **

**Distance **

Jaywalking 

0.488 \(0.333\) 

0.730 \(0.450\) 

0.676 \(0.569\) 

0.595 \(0.547\) 

Non-Jaywalking 

0.432 \(0.130\) 

0.705 \(0.370\) 

0.711 \(0.840\) 

0.562 \(0.388\) 

Note 1: Standard deviations are provided in parentheses. 

Note 2: The differences in accuracy are not statistically significant at the 95% confidence level for all variables. 

****

**4.3.2 Trajectory Analysis **

Figure 4.6** **presents two distinct instances of pedestrian-vehicle conflicts. Figure 4.6\(a\)** **is derived from the jaywalking pedestrian-vehicle conflict model while Figure 4.6\(b\) considers the non-jaywalking pedestrian-vehicle model. The figure illustrates the simulated trajectories of both pedestrians and vehicles, which show the models’ ability to replicate the road users’ evasive actions with high accuracy. 

In Figure 4.6\(a\), the behavior of the jaywalking pedestrian is characterized by a slow pace, which is accurately captured by the simulation model, and the vehicle exhibits a similar speed pattern throughout the trajectory. This is evident in the speed plots where the blue line \(actual vehicle speed\) closely aligns with the orange line \(simulated vehicle speed\), and the green line \(actual pedestrian speed\) corresponds well with the red line \(simulated pedestrian speed\). Additionally, at the beginning of the interaction, the simulated driver performs a swerving maneuver as part of 67 





an evasive action strategy. Furthermore, the trajectory of the jaywalking pedestrian reveals instability, which highlights the erratic nature of the movements and is effectively represented in the simulated model. However, it is important to note that the simulation model introduced an additional swerving maneuver for the pedestrian, which is evident from the deviation of the red line \(simulated pedestrian position\) from the blue line \(actual pedestrian position\). Still, it shows that the evasive action behavior mechanism is accurately represented. ** **Figure 4.6\(b\) presents a scenario involving a non-jaywalking pedestrian who accelerates as it approaches the vehicle, which is effectively captured in the simulated trajectory and demonstrates the model's capability to represent realistic pedestrian behavior. The vehicle follows a similar speed pattern throughout the trajectory, as in the jaywalking case. In the simulated trajectory, the pedestrian performs an additional evasive maneuver, increasing its distance from the vehicle, which highlights the proactive measures to ensure safety. Moreover, the lateral displacement of the pedestrian appears delayed relative to the actual trajectory, indicating a temporal lag in the model response. This shows that, while the timing of evasive maneuvers might require refinement, the overall movement trends are captured. 

68 





**\(a\) Jaywalking Pedestrian-Vehicle Interaction **



**\(b\) Non-Jaywalking Pedestrian-Vehicle Interaction **

**Figure 4.6 Trajectory Simulations for Pedestrian-Vehicle Interactions** 69 





**4.3.3 Evasive Action Assessment **

Evasive actions were also considered to evaluate the accuracy of the simulated models. Both speed changes and directional changes were analyzed. For speed changes, road users could accelerate, decelerate, or maintain a steady speed. Similarly, for directional changes, they could either keep their current directions or alter them. To assess the models’ effectiveness, the actual and simulated trajectories of road users were compared, and the accuracy of the models was quantitatively assessed by calculating the percentage of evasive actions that were correctly predicted by the simulation model when compared to the actual behavior. The accuracy was determined by reviewing each road user’s trajectory and comparing the observed trajectory with the simulated one. If the observed and simulated trajectories followed the same trend for acceleration \(up for acceleration, down for deceleration, or steady for no change\) and yaw \(whether the trajectory direction remained the same\), the action was considered accurately predicted. The accuracy was then expressed as the ratio of correct predictions to the total number of observed evasive actions. Confusion matrices were then used to visualize the performance of the model by displaying the counts of true positive, true negative, false positive, and false negative predictions for each category. 





70 





Table 4.3 and Table 4.4 present the confusion matrices for the jaywalking pedestrian-vehicle model. For pedestrians, the confusion matrix reveals accuracies of 87% and 83% for acceleration-based yaw-rate maneuvers, respectively, which indicates that the model effectively captured the pedestrians’ responses in jaywalking scenarios. For vehicles, the accuracy for acceleration-based maneuvers was 72%, while yaw-rate maneuvers achieved an accuracy of 81%. These results highlight the model's capability to simulate how vehicles adapt to unpredictable pedestrian behaviors. 





71 





Table 4.5 and Table 4.6 display the confusion matrices for the non-jaywalking pedestrian-vehicle model. The pedestrian confusion matrices indicate an accuracy of 90% for acceleration-based maneuvers and 82% for yaw-rate maneuvers, which reflects a great alignment between the simulated and actual pedestrian behaviors. Conversely, the vehicle confusion matrices show accuracies of 77% and 89%, respectively, for acceleration-based and yaw-rate maneuvers, which underscores the models’ effectiveness in simulating vehicle behaviors in non-jaywalking scenarios. 

These results demonstrate that predicting road user behavior in non-jaywalking scenarios was generally easier when compared to jaywalking scenarios. This emphasizes the challenges in accurately modeling scenarios where human behavior deviates from the expected norms, which shows the need for further refinement of existing simulation models to enhance predictive accuracy in complex real-world scenarios. 



****

72 





**Table 4.3 Vehicle Confusion Matrix in the Jaywalking Pedestrian-Vehicle Model** Simulated Jaywalking Vehicle 



Acceleration 

Deceleration 

No Change 

Acceleration 

43 

17 

9 

Deceleration 

1 

23 

0 

Actual 

No Change 

0 

2 

7 

Jaywalking 



Yaw Rate Change 

No Yaw Rate Change 

Vehicle 

Yaw Rate 

31 

0 

Change 

No Yaw Rate 

19 

52 

Change 

****

**Table 4.4 Pedestrian Confusion Matrix in the Jaywalking Pedestrian-Vehicle Model** Simulated Jaywalking Pedestrian 



Acceleration 

Deceleration 

No Change 

Acceleration 

31 

6 

4 

Deceleration 

1 

43 

1 

Actual 

No Change 

0 

2 

14 

Jaywalking 



Yaw Rate Change 

No Yaw Rate Change 

Pedestrian 

Yaw Rate 

47 

0 

Change 

No Yaw Rate 

17 

38 

Change 





****

73 





**Table 4.5 Vehicle Confusion Matrix in the Non-Jaywalking Pedestrian-Vehicle Model** Simulated Non-Jaywalking Vehicle 



Acceleration 

Deceleration 

No Change 

Acceleration 

32 

13 

6 

Deceleration 

0 

18 

0 

Actual Non-

No Change 

1 

2 

25 

Jaywalking 



Yaw Rate Change 

No Yaw Rate Change 

Vehicle 

Yaw Rate 

8 

0 

Change 

No Yaw Rate 

11 

78 

Change 

****

**Table 4.6 Pedestrian Confusion Matrix in the Non-Jaywalking Pedestrian-Vehicle Model** Simulated Non-Jaywalking Pedestrian 



Acceleration 

Deceleration 

No Change 

Acceleration 

20 

2 

3 

Deceleration 

3 

40 

0 

Actual Non-

No Change 

0 

2 

27 

Jaywalking 



Yaw Rate Change 

No Yaw Rate Change 

Pedestrian 

Yaw Rate 

37 

0 

Change 

No Yaw Rate 

17 

43 

Change 





74 





**4.3.4 Severity Analysis **

Figure 4.7 and Figure 4.8 illustrate the PET and TTC distributions of the simulated trajectories after applying the multiagent policies to the non-jaywalking dataset. In other words, the non-jaywalking dataset is considered as a baseline, and the multiagent policies of both the jaywalking model and of the non-jaywalking model are considered to simulate road user trajectories. For both conflict indicators, lower values indicate more severe conflicts. The results show that applying jaywalking multiagent policies to the baseline increases conflict severity, as shown by lower PET and TTC values. This observation suggests that jaywalking behaviors are associated with increased risk, as shown by average reductions of 58% and 16% on the PET and TTC 

values, respectively. Therefore, jaywalking interactions inherently lead to more severe conflicts, as consistent with previous studies \(Ansariyar & Jeihani, 2023; Zhang et al., 2023\). 

**0.3**

**0.2**

**Density**

**0.1**

**0.0**

**0**

**1**

**2**

**3**

**4**

**5**

**PET \(s\)**

**Jaywalking**

**Non−Jaywalking**



**Figure 4.7 Conflict Severity PET Distribution Simulation Comparison** 75 





**0.75**

**0.50**

**Density**

**0.25**

**0.00**

**0.0**

**0.5**

**1.0**

**1.5**

**2.0**

**2.5**

**3.0**

**3.5**

**4.0**

**4.5**

**5.0**

**TTC \(s\)**

**Jaywalking**

**Non−Jaywalking**



**Figure 4.8 Conflict Severity TTC Distribution Simulation Comparison** **4.4 Turning Vehicle Interaction Simulation Model **

To further evaluate differences in behavior between non-jaywalking and jaywalking pedestrians, an additional simulation environment was developed to obtain pedestrian-vehicle conflicts in right-turns. The simulation setup begins with predefined initial and final positions, in addition to heading angles and sampled speeds based on normal distributions with mean and standard deviation values from Table 4.1. These initial and final positions of both road users were defined based on the dimensions of the study area. Similar to the simulation platform to replicate road user behavior, these parameters allow for calculating the necessary state features to derive optimal policies and update both positions and speeds. Figure 4.9 illustrates the scenario with a pedestrian crossing the road while a vehicle performs a right turn. A total of 10,000 simulations were run, and the resulting variable distributions from these simulated scenarios are shown in Figure 4.10, with corresponding descriptive statistics summarized in Table 4.7. 

76 





***Pedestrian***

***Ini1al Posi1on: \(2,10\)***

***Right-Turn Vehicle***

***Final Posi1on: \(14,14\)***

***Pedestrian***

***Final Posi1on: \(2,3\)***

***Right-Turn Vehicle***

***Ini1al Posi1on: \(0,0\)***



**Figure 4.9 Simulated Pedestrian-Vehicle Right-Turn Scenarios** The results of the right-turn simulation for pedestrian-vehicle interactions reveal distinct patterns between jaywalking and non-jaywalking scenarios considering various metrics, including TTC, PET, minimum distance, speed, acceleration, and yaw rate. T-tests and F-tests were performed to assess the statistical significance of these differences, and they confirmed that all measured variables were significantly different when comparing the non-jaywalking simulation model to the jaywalking simulation model. 

In jaywalking scenarios, the average PET is considerably lower at 1.336 s when compared to 3.237 s for non-jaywalking scenarios. The shorter average PET in jaywalking scenarios is associated with a higher conflict severity, as it indicates that pedestrians and vehicles are in closer proximity and would collide more quickly if their paths remained unchanged. Jaywalking pedestrians often cross unpredictably, leading to more immediate risks and faster vehicle 77 





responses to avoid crashes. In contrast, non-jaywalking scenarios exhibit longer PETs, which leads to vehicles having greater time windows to adjust their speeds or trajectories. Additionally, the average TTC in jaywalking scenarios is slightly shorter at 1.416 seconds when compared to 1.485 seconds for non-jaywalking interactions. Similarly, the lower TTC in jaywalking scenarios demonstrates a higher severity, as it indicates that pedestrians and vehicles are in closer proximity and would collide more quickly if their paths remained unchanged. Jaywalking simulated interactions show a lower average minimum distance of 1.286 m between pedestrians and drivers, in contrast to 1.574 m in non-jaywalking scenarios. This closer proximity in the jaywalking pedestrian-vehicle model suggests a higher risk, as consistent with previous studies \(Lanzaro et al., 2023\). Non-jaywalking pedestrians maintain slightly safer buffers, which aligns with their more predictable crossing patterns that allow drivers to anticipate their movements more comfortably. 

Jaywalking interactions display higher speeds for both pedestrians and drivers, with pedestrians averaging 2.033 m/s and drivers 3.950 m/s. These elevated speeds suggest that pedestrians may cross more quickly to minimize the time spent on the road. Drivers also travel slightly faster in these interactions, possibly due to the unpredictable nature of jaywalking crossings, where both road users prioritize clearing the conflict zone more quickly. In non-jaywalking scenarios, both pedestrians and vehicles adopt slower speeds, averaging 1.784 m/s and 3.118 m/s, respectively. 

These slower speeds in non-jaywalking scenarios reflect more predictable interactions between road users, as also shown by the smaller standard deviations in acceleration. For example, the standard deviations in acceleration for the non-jaywalking pedestrian-vehicle model considering vehicles \(4.453 m/s²\) and pedestrians \(2.752 m/s²\) are lower than for the jaywalking pedestrian-78 





vehicle model in terms of vehicles \(4.958 m/s²\) and pedestrians \(3.330 m/s²\). In non-jaywalking scenarios, the lower variability in acceleration means that both pedestrians and vehicles are more consistent in their movements, which allows for better anticipation of each other’s actions and reduces the need for abrupt speed changes. This results in more controlled interactions compared to the more reactive behavior in jaywalking scenarios. 

Finally, the yaw rate results show that jaywalking pedestrians have lower yaw rates \(1.299 rad/s\) compared to non-jaywalking pedestrians \(3.246 rad/s\), suggesting that jaywalking pedestrians make fewer directional adjustments as they cross. This indicates that they are less likely to take evasive actions in response to surrounding traffic. Similarly, vehicles in jaywalking scenarios exhibit lower yaw rates \(2.026 rad/s\) compared to non-jaywalking scenarios \(2.663 rad/s\), suggesting that drivers do not adjust their trajectories as much when interacting with jaywalking pedestrians. In contrast, in non-jaywalking scenarios, both pedestrians and vehicles demonstrate higher yaw rates, which reflects more frequent changes in direction as they respond to each other’s movements. This suggests that non-jaywalking pedestrians, who typically follow structured paths, are more aware of their surroundings and adjust their trajectories accordingly when faced with potential conflicts. 

Overall, these results highlight that jaywalking interactions are characterized by lower TTC and PET values, indicating more severe conflicts and reduced time for evasive maneuvers. These interactions also involve closer proximity, higher speeds, abrupt accelerations, and limited directional adjustments, suggesting that jaywalking pedestrians tend to maintain their trajectories with minimal directional change evasive actions, potentially due to lower situational awareness, but considerable speed changes. Conversely, in non-jaywalking scenarios, the interactions 79 





present longer TTC and PET values, greater buffer distances, lower speeds, smoother accelerations, and more frequent directional changes. These behaviors indicate safer and more predictable interactions between pedestrians and drivers. 



1.25

1.5

1.00

1.0

0.75

0.50

0.5

Density

Density 0.25

0.0

0.00

0

1

2

3

4

5

0

1

2

3

4

5

PET \(s\)

TTC \(s\)

Jaywalking

Non−Jaywalking

Jaywalking

Non−Jaywalking

1.5

2.0

1.5

1.0

1.0

0.5

Density 0.5

Density

0.0

0.0

0

2

4

1

2

3

4

Distance \(m\)

Pedestrian Speed \(m/s\)

Jaywalking

Non−Jaywalking

Jaywalking

Non−Jaywalking

0.3

0.3

0.2

0.2

0.1

Density

0.1

Density

0.0

0.0

0

4

8

0.0

2.5

5.0

7.5

10.0

Vehicle Speed \(m/s\)

Absolute Pedestrian Acceleration \(m/s²\)

Jaywalking

Non−Jaywalking

Jaywalking

Non−Jaywalking

0.15

0.75

0.10

0.50

0.05

Density

0.25

Density

0.00

0.00

0

5

10

15

0

2

4

6

8

Absolute Vehicle Acceleration \(m/s²\)

Absolute Pedestrian Yaw \(rad/s\)

Jaywalking

Non−Jaywalking

Jaywalking

Non−Jaywalking



**Figure 4.10 Simulated Pedestrian-Vehicle Right-Turn Interactions Distributions** 80 





**Table 4.7 Simulated Pedestrian-Vehicle Right-Turn Interactions Behavioral Statistics** **Jaywalking Pedestrian-Vehicle **

**Non-Jaywalking Pedestrian-Vehicle **

**Variable **

**Interactions **

**Interactions **

**Vehicle **

**Pedestrian **

**Vehicle **

**Pedestrian **

Post-Encroachment-

1.336 \(0.756\) 

3.237 \(1.025\) 

Time \(s\) 

Time-to-Collision \(s\) 

1.416 \(0.401\) 

1.485 \(0.330\) 

Minimum Distance 

1.286 \(0.480\) 

1.574 \(1.500\) 

\(m\) 

Speed \(m/s\) 

3.950 \(3.207\) 

2.033 \(0.672\) 

3.118 \(2.706\) 

1.784 \(1.118\) 

Acceleration \(m/s2\) 

6.192 \(4.958\) 

3.760 \(3.330\) 

4.964 \(4.453\) 

4.683 \(2.752\) 

Yaw Rate \(rad/s\) 

2.026 \(2.118\) 

1.299 \(1.361\) 

2.663\(2.038\) 

3.246 \(1.834\) 

\* Standard deviations are provided in parentheses. 

\* All variables are statistically significantly different at the 95% confidence level. 





81 





## Chapter 5: Conclusion 

This section summarizes the key findings of this study, focusing on the insights gained from modeling jaywalking and non-jaywalking behavior using Multiagent Adversarial Inverse Reinforcement Learning \(MAAIRL\) and highlighting their differences. Subsequently, the contributions outline the study's practical implications for safety. Finally, the limitations and the future research directions address study constraints and suggest potential improvements for the future. 

**5.1 Summary **

This study used MAAIRL to model jaywalking behavior in vehicle-pedestrian interactions using data from a signalized intersection in Vancouver, Canada. This framework enabled \(1\) estimating reward functions that provide inferences into road user behavior in conflict situations and \(2\) obtaining optimal policies that represent the best sequence of decisions for both pedestrians and vehicles. To evaluate the model performance, different platforms were developed to replicate road user behavior and simulate their trajectories. Additionally, the results provide insights into how jaywalking influences conflict severity and the evasive actions of both pedestrians and drivers. Simulated jaywalking pedestrian trajectories are crucial for understanding how pedestrians behave in unpredictable situations and how vehicles respond to them. Pedestrian simulation models allow for proactive safety measures by informing traffic management strategies and infrastructure design to reduce severe conflicts. Furthermore, these models can support signal timing optimization, the design of safer intersections, and the development of automated vehicle technologies that better anticipate pedestrian actions, especially in unpredictable situations such as jaywalking. 

82 





The reward function analysis revealed key distinctions in speed, lateral distance, and interaction angles between jaywalking and non-jaywalking interactions. In non-jaywalking scenarios, pedestrians exhibited structured behavior, increasing their speed as they approached the conflict point and decelerating afterward, which indicates confidence in their safety and predictability in movement. In contrast, jaywalking pedestrians demonstrated more erratic speed patterns, initially approaching the conflict point cautiously before accelerating sharply post-interaction to minimize their exposure to potential vehicle conflicts. Also, non-jaywalking pedestrians initially stayed closer to vehicles but increased their lateral distance as they neared the conflict point, which suggests increased risk perception during the interaction moment. Jaywalking pedestrians, however, maintained smaller lateral distances throughout their trajectories, prioritizing efficiency over safety. Moreover, non-jaywalking crossings presented larger interaction angles, which enhanced visibility and predictability for both pedestrians and drivers, whereas jaywalking pedestrian movements often occurred at smaller interaction angles, reducing the communication between road users. For drivers, controlled speed adjustments were evident in non-jaywalking scenarios, where they slowed down before the interactions and accelerated after them. In jaywalking scenarios, drivers exhibited greater caution, maintaining smaller speed increases and larger lateral distances due to the unpredictability of pedestrian behavior. 

The MAAIRL model was able to effectively simulate pedestrian trajectories and capture the behavior of jaywalking pedestrians, more specifically their unpredictable movements and the increased conflict risk. Additionally, the NRMSE values showed that the MAAIRL framework presented no significant discrepancies in predicting the behavior of road users when comparing jaywalking and non-jaywalking scenarios. The evasive actions assessment further confirmed the 83 





models' effectiveness in predicting road user responses. In jaywalking scenarios, the simulation successfully predicted the need for pedestrians to alter their speeds and directions to avoid crashes, with accuracies of 87% and 83%, respectively. The accuracies of vehicle responses to jaywalking pedestrians were slightly lower \(i.e., 72% and 81% for acceleration-based and yaw-rate-based maneuvers, respectively\). Conversely, in non-jaywalking scenarios, the simulation accurately predicted the need for pedestrians to adjust their speeds and directions with rates of 90% and 82%, respectively. Similarly, the accuracies of vehicle responses to non-jaywalking pedestrians were lower, with 77% for acceleration-based maneuvers and 89% for yaw rate-based maneuvers. The right-turn simulations provided additional insights into how jaywalking impacts the safety of the interactions. The analysis showed that, in jaywalking scenarios, the conflict severity was higher, with shorter TTCs and PETs, lower minimum distances between road users, and faster pedestrian movements. These results suggest the increased risks associated with jaywalking, where quicker reactions are required from both pedestrians and drivers. Conversely, in non-jaywalking scenarios, drivers had more time to adjust their trajectories and could execute smoother, less abrupt maneuvers. 

**5.2 Contributions **

The findings from this study have significant implications for traffic safety, particularly in areas where pedestrian-vehicle conflicts are common and jaywalking is prevalent. For example, the simulation results highlight the need for improved traffic management strategies to address high-risk scenarios, such as opportunities to optimize signal timings and improve intersection designs. 

Previous studies have shown that longer pedestrian signal durations can significantly reduce jaywalking by accommodating pedestrian crossing needs \(Zhuang & Wu, 2011\). Additionally, 84 





measures such as Leading Pedestrian Intervals \(LPIs\), adaptive signal controls, and exclusive pedestrian phases can be explored to further reduce conflicts. LPIs, in particular, have been found to reduce the rate of pedestrian-vehicle conflicts during both the leading phase and the remainder of the walk phase, as well as decrease vehicular non-yield behavior and pedestrian noncompliance once pedestrians are familiar with the LPI operation \(Saneinejad & Lo, 2015\). 

Finally, considering intersection design, restricting right-turns-on-red, implementing tighter curb radii, and building pedestrian refuge islands can enhance safety by reducing vehicle speeds and minimizing pedestrian exposure to conflicts, which are key contributors to jaywalking behavior \(Harwood et al., 2008; Saneinejad & Lo, 2015\) 

In addition to intersection design, this study also provides methodological contributions by demonstrating the effectiveness of MAAIRL in capturing the decision-making processes of both pedestrians and drivers. Unlike traditional models that rely on predefined behavioral assumptions, the inverse reinforcement learning approach enables a clear understanding of road user incentives, making it an adaptable framework for different urban environments. This methodology could be extended to evaluate the impact of various countermeasures by simulating behavioral responses to new interventions. This approach allows for low cost evaluations without requiring real-world implementation, making it an efficient tool for assessing potential safety measures before deployment. Additionally, by accurately capturing road user behavior and conflicts at significantly short time intervals, the model provides granular insights into the dynamics of pedestrian-vehicle interactions. This capability ensures a detailed and realistic representation of traffic scenarios, improving the reliability of safety interventions. 

85 





Furthermore, this study contributes to proactive road safety analysis by integrating simulation-based risk assessment with real-world trajectory data. The ability to simulate near-miss conflicts with high accuracy supports the development of predictive safety models, which can be instrumental in assessing potential crash risks before they materialize. By identifying and analyzing these near-miss events, decision-makers can proactively implement interventions to mitigate future crashes. Conflicts are strongly associated with crashes based on the pyramid of traffic events, where minor interactions escalate into more severe outcomes. By accurately simulating conflicts, this study provides a valuable tool for estimating crash risks with minimal cost, reducing the need for expensive and time-consuming field studies. 

**5.3 Limitations and Future Research **

There are several limitations in this study. While this research focused on the behavior of right-turning vehicles, future research could expand to include a broader range of traffic movements and more complex intersection configurations. Also, the study used data from Downtown Vancouver, Canada, and other locations can be further investigated as culture plays an important role in traffic. Pedestrian behavior, jaywalking tendencies, and driver responses may vary significantly across different urban environments, particularly in cities with diverse regulatory frameworks, enforcement levels, and infrastructure conditions. Moreover, this study used the logistic best response equilibrium structure applied to an inverse reinforcement learning approach, and alternate methods such as diffusion models can be applied. Future research could also evaluate and compare the performance of other equilibrium solution concepts to further refine modeling techniques. Additionally, future work can examine how the findings vary across different signal phases, such as Steady "Walk," Flashing "Don't Walk" \(FDW\), Buffer Interval, 86 





and Steady "Don't Walk" \(DW\). Analyzing how pedestrian hesitation, start-up delay, and crossing speed differ across these phases could offer deeper insights into behavioral adaptations. 

Additionally, this research focused on jaywalking limited to the context of walking during prohibited signal phases at signalized intersections. This method could be applied to jaywalking in the context of mid-block crossings, where pedestrian behavior may be influenced by factors such as median refuges, road width, and gaps in traffic. Moreover, analyzing interactions at unsignalized crossings or areas with pedestrian-activated signals could further broaden the applicability of this approach. 

Another limitation of this study is the lack of consideration of pedestrian demographics, such as age, gender, and other factors. Pedestrian behavior, including jaywalking tendencies, may differ across these demographic groups. Future research could include a breakdown of pedestrian demographics and compare how these variables influence jaywalking behavior. Additionally, this study assumes that pedestrian and driver behavior remain static across different environmental conditions. Factors such as weather, lighting conditions, and infrastructure quality could influence decision-making. Expanding the dataset to include nighttime and adverse weather conditions could improve the generalizability of the findings. This approach could also explore the influence of different peak hours, where higher traffic and pedestrian volumes may affect the severity and the frequency of conflicts. Finally, this study primarily focused on pedestrian and vehicle interactions in the context of individual decision-making. Future work could explore the role of group behavior in jaywalking scenarios, as pedestrians often make crossing decisions collectively rather than individually. Investigating social influences, such as peer pressure or crowd dynamics, could provide further insights into jaywalking tendencies. 

87 





As emerging technologies such as connected vehicle systems and pedestrian detection sensors become more prevalent, future studies could assess how these innovations influence pedestrian-vehicle interactions. Future research could explore how AVs can accommodate jaywalking by examining AV interactions with pedestrians who jaywalk, and how AV technology can help reduce jaywalking incidents or adjust to pedestrian behavior in real-time. Understanding the extent to which technology-assisted warning systems alter road user behavior \(by reducing jaywalking frequency, improving driver response times, or mitigating conflict severity\) could help refine traffic management strategies and enhance safety interventions. Ultimately, a multidisciplinary approach that integrates behavioral science, machine learning, and real-world policy interventions will be essential for developing comprehensive strategies that address the complexities of jaywalking and pedestrian safety in evolving traffic environments. 



88 





**Bibliography **

AASHTO. \(2010\). *Highway Safety Manual* \(1st Edition\). American Association of State Highway Transportation Officials. 

Aden, W. A., Zhao, S., Subhan, F., Zhou, H., & Ullah, I. \(2020\). A Comparative Study on Pedestrians’ Intention to Violate Traffic Rules: The Case of China and Djibouti. *Journal* *of Road and Traffic Engineering*, *66*\(3\), Article 3. https://doi.org/10.31075/PIS.66.03.01 

Alhajyaseen, W. K. M., & Iryo-Asano, M. \(2017\). Studying critical pedestrian behavioral changes for the safety assessment at signalized crosswalks. *Safety Science*, *91*, 351–360. 

https://doi.org/10.1016/j.ssci.2016.09.002 

Allen, B. L., Shin, B. T., & Cooper, P. J. \(1978\). ANALYSIS OF TRAFFIC CONFLICTS AND 

COLLISIONS. *Transportation Research Record*, *667*, Article HS-025 846. 

https://trid.trb.org/View/85806 

Alsaleh, R., & Sayed, T. \(2020\). Modeling pedestrian-cyclist interactions in shared space using inverse reinforcement learning. *Transportation Research Part F: Traffic Psychology and* *Behaviour*, *70*, 37–57. https://doi.org/10.1016/j.trf.2020.02.007 

Alsaleh, R., & Sayed, T. \(2021a\). Markov-game modeling of cyclist-pedestrian interactions in shared spaces: A multi-agent adversarial inverse reinforcement learning approach. 

*Transportation Research Part C: Emerging Technologies*, *128*, 103191. 

https://doi.org/10.1016/j.trc.2021.103191 

Alsaleh, R., & Sayed, T. \(2021b\). Microscopic Modeling of Cyclists Interactions with Pedestrians in Shared Spaces: A Gaussian Process Inverse Reinforcement Learning Approach. *Transportmetrica A: Transport Science*, *18*\(1\). 

https://doi.org/10.1080/23249935.2021.1898487 

89 





Alsaleh, R., Sayed, T., & Zaki, M. H. \(2018\). Assessing the Effect of Pedestrians’ Use of Cell Phones on Their Walking Behavior: A Study Based on Automated Video Analysis. 

*Transportation Research Record*, *2672*\(35\), 46–57. 

https://doi.org/10.1177/0361198118780708 

Alsharif, T., Lanzaro, G., & Sayed, T. \(2024\). Distracted Walking: Does it impact pedestrian-vehicle interaction behavior? *Accident Analysis & Prevention*, *208*, 107789. 

https://doi.org/10.1016/j.aap.2024.107789 

Amodei, D., Olah, C., Steinhardt, J., Christiano, P., Schulman, J., & Mané, D. \(2016\). *Concrete* *Problems in AI Safety* \(No. arXiv:1606.06565\). arXiv. 

https://doi.org/10.48550/arXiv.1606.06565 

Amundsen, F. H., & Hydén, C. \(1977\). *Proceedings of the 1st Workshop on Traffic Conflicts. * 

Andrade Lanzaro, G. \(2021\). *Modelling motorcyclist-pedestrian interactions using inverse* *reinforcement learning* \[PhD Thesis, University of British Columbia\]. 

https://open.library.ubc.ca/soa/cIRcle/collections/ubctheses/24/items/1.0401892 

Anik, M. A. H., Hossain, M., & Habib, M. A. \(2021\). Investigation of pedestrian jaywalking behaviour at mid-block locations using artificial neural networks. *Safety Science*, *144*, 105448. https://doi.org/10.1016/j.ssci.2021.105448 

Ansariyar, A., & Jeihani, M. \(2023\). STATISTICAL ANALYSIS OF JAYWALKING 

CONFLICTS BY A LIDAR SENSOR. *Scientific Journal of Silesian University of* *Technology. Series Transport*, *120*, 17–36. https://doi.org/10.20858/sjsutst.2023.120.2 

Antonini, G., Bierlaire, M., & Weber, M. \(2004\). *Simulation of Pedestrian Behaviour using a* *Discrete Choice Model Calibrated on Actual Motion Data*. 

90 





https://www.semanticscholar.org/paper/Simulation-of-Pedestrian-Behaviour-using-a-Discrete-Antonini-Bierlaire/46665e5adc643bd8dfb55bb2addbd4b57bb93171 

Antonini, G., Bierlaire, M., & Weber, M. \(2006\). Discrete choice models of pedestrian walking behavior. *Transportation Research Part B: Methodological*, *40*\(8\), 667–687. 

https://doi.org/10.1016/j.trb.2005.09.006 

Anvari, B., Bell, M. G. H., Sivakumar, A., & Ochieng, W. Y. \(2015\). Modelling shared space users via rule-based social force model. *Transportation Research Part C: Emerging* *Technologies*, *51*, 83–103. https://doi.org/10.1016/j.trc.2014.10.012 

Archer, J. \(2005\). *Indicators for traffic safety assessment and prediction and their application in* *micro-simulation modelling: A study of urban and suburban intersections*. 

https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-143 

Aumann, R. J. \(1974\). Subjectivity and correlation in randomized strategies. *Journal of* *Mathematical Economics*, *1*\(1\), 67–96. https://doi.org/10.1016/0304-4068\(74\)90037-8 

Autey, J., Sayed, T., & Zaki, M. H. \(2012\). Safety evaluation of right-turn smart channels using automated traffic conflict analysis. *Accident Analysis & Prevention*, *45*, 120–130. 

https://doi.org/10.1016/j.aap.2011.11.015 

Bansal, A., Goyal, T., & Sharma, U. \(2022\). Pragmatic Modeling of Pedestrian Jay walking Behaviour at Signalised Intersections in Urban Area. *Indian Journal of Engineering and* *Materials Sciences \(IJEMS\)*, *28*\(6\), Article 6. https://doi.org/10.56042/ijems.v28i6.44166 

Bella, F., & Nobili, F. \(2020\). \(PDF\) Driver-pedestrian interaction under legal and illegal pedestrian crossings. *Transportation Research Procedia*, *45*\(4\). 

https://doi.org/10.1016/j.trpro.2020.03.038 

91 





Brechtel, S., Gindele, T., & Dillmann, R. \(2011\). Probabilistic MDP-behavior planning for cars. 

*2011 14th International IEEE Conference on Intelligent Transportation Systems \(ITSC\)*, 1537–1542. https://doi.org/10.1109/ITSC.2011.6082928 

Brubacher, J. R., Chan, H., & Erdelyi, S. \(2019\). Injury severity in police collision reports correlates poorly with requirement for hospital admission. *Journal of Transport &* *Health*, *14*, 100606. https://doi.org/10.1016/j.jth.2019.100606 

Burstedde, C., Klauck, K., Schadschneider, A., & Zittartz, J. \(2001\). Simulation of pedestrian dynamics using a two-dimensional cellular automaton. *Physica A: Statistical Mechanics* *and Its Applications*, *295*\(3\), 507–525. https://doi.org/10.1016/S0378-4371\(01\)00141-8 

Chattaraj, U., Seyfried, A., & Chakroborty, P. \(2009\). *Comparison of Pedestrian Fundamental* *Diagram Across Cultures* \(No. arXiv:0903.0149\). arXiv. 

https://doi.org/10.48550/arXiv.0903.0149 

Cheng, W., Zhang, N., Li, W., & Xi, J. \(2014\). Modeling and Application of Pedestrian Safety Conflict Index at Signalized Intersections. *Discrete Dynamics in Nature and Society*, *2014*, 1–6. 

Chin, H.-C., & Quek, S.-T. \(1997\). Measurement of traffic conflicts. *Safety Science*, *26*\(3\), 169–

185. https://doi.org/10.1016/S0925-7535\(97\)00041-6 

Choi, J., Kim, S., Kim, S., Hong, H., & Baik, S. \(2013\). *PEDESTRIAN CRASHES DURING *

*JAYWALKING, CAN WE AFFORD TO OVERLOOK? * 

Committee on Transportation and Infrastructure. \(2024\). *The New York City Council—File \#: Int* *0346-2024*. 

https://legistar.council.nyc.gov/LegislationDetail.aspx?ID=6557803&GUID=7D6F4CEC

-85C3-4E00-9E54-36641179493B 

92 





Coropulis, S., Berloco, N., Gentile, R., Intini, P., & Ranieri, V. \(2024\). Traffic microsimulation for road safety assessments of vehicle automation scenarios: Model comparison and sensitivity analysis. *Simulation Modelling Practice and Theory*, *130*, 102868. 

https://doi.org/10.1016/j.simpat.2023.102868 

Cunto, F., & Saccomanno, F. F. \(2008\). Calibration and validation of simulated vehicle safety performance at signalized intersections. *Accident Analysis & Prevention*, *40*\(3\), 1171–

1179. https://doi.org/10.1016/j.aap.2008.01.003 

Dias, C., Iryo-Asano, M., Nishiuchi, H., & Todoroki, T. \(2018\). Calibrating a social force based model for simulating personal mobility vehicles and pedestrian mixed traffic. *Simulation* *Modelling Practice and Theory*, *87*, 395–411. 

https://doi.org/10.1016/j.simpat.2018.08.002 

El Hamdani, S., Loudari, S., Novotny, S., Bouchner, P., & Benamar, N. \(2021\). A Markov Decision Process Model for a Reinforcement Learning-based Autonomous Pedestrian Crossing Protocol. *2021 3rd IEEE Middle East and North Africa COMMunications* *Conference \(MENACOMM\)*, 147–151. 

https://doi.org/10.1109/MENACOMM50742.2021.9678310 

El-Basyouny, K. \(2011\). *New techniques for developing safety performance functions* 

\[University of British Columbia\]. https://doi.org/10.14288/1.0063049 

Elvik, R., & Mysen, A. B. \(1999\). Incomplete Accident ReportingMeta-Analysis of Studies Made in 13 Countries. *Transportation Research Record 1665*, *99–0047*, 133–140. 

Erol, K., Levy, R., & Wentworth, J. \(1998\). Application of agent technology to traffic simulation. *Intelligent Systems and Interfaces*. 

93 





Essa, M., & Sayed, T. \(2015a\). Simulated Traffic Conflicts: Do They Accurately Represent Field-Measured Conflicts? *Transportation Research Record: Journal of the* *Transportation Research Board*, *2514*, Article 15–0707. 

https://trid.trb.org/View/1336747 

Essa, M., & Sayed, T. \(2015b\). Transferability of calibrated microsimulation model parameters for safety assessment using simulated conflicts. *Accident Analysis & Prevention*, *84*, 41–

53. https://doi.org/10.1016/j.aap.2015.08.005 

Fan, R., Yu, H., Liu, P., & Wang, W. \(2013\). Using VISSIM simulation model and Surrogate Safety Assessment Model for estimating field measured traffic conflicts at freeway merge areas. *IET Intelligent Transport Systems*, *7*\(1\), 68–77. 

Farina, F., Fontanelli, D., Garulli, A., Giannitrapani, A., & Prattichizzo, D. \(2017\). Walking Ahead: The Headed Social Force Model. *PloS One*, *12*\(1\), e0169734. 

https://doi.org/10.1371/journal.pone.0169734 

Finn, C., Levine, S., & Abbeel, P. \(2016\). *Guided Cost Learning: Deep Inverse Optimal Control* *via Policy Optimization* \(No. arXiv:1603.00448\). arXiv. 

https://doi.org/10.48550/arXiv.1603.00448 

Fu, J., Luo, K., & Levine, S. \(2017\). *Learning Robust Rewards with Adversarial Inverse* *Reinforcement Learning* \(No. arXiv:1710.11248\). arXiv. 

https://doi.org/10.48550/arXiv.1710.11248 

Geiger, A., Lenz, P., & Urtasun, R. \(2012\). Are we ready for autonomous driving? The KITTI Vision Benchmark Suite. *ResearchGate*. Computer Vision and Pattern Recognition \(CVPR\), 2012 IEEE Conference on. https://doi.org/10.1109/CVPR.2012.6248074 

94 





Gettman, D., Head, L., & Siemens Gardner Transportation Systems. \(2003\). *Surrogate safety* *measures from traffic simulation models* \(No. FHWA-RD-03-050\). 

https://rosap.ntl.bts.gov/view/dot/1005 

Gettman, D., Pu, L., Sayed, T., Shelby, S. G., & Siemens Energy and Automation. Business Unit Intelligent Transportation Systems. \(2008\). *Surrogate Safety Assessment Model and* *Validation: Final Report* \(No. FHWA-HRT-08-051\). 

https://rosap.ntl.bts.gov/view/dot/39210 

Ghoul, T. \(2021\). *Exploring the applications of connected vehicle data to real time safety* *optimization at isolated intersections* \[University of British Columbia\]. 

https://doi.org/10.14288/1.0401847 

Guo, H., Wang, W., Guo, W., Jiang, X., & Bubb, H. \(2012\). Reliability analysis of pedestrian safety crossing in urban traffic environment. *Safety Science*, *50*\(4\), 968–973. 

https://doi.org/10.1016/j.ssci.2011.12.027 

Guo, R.-Y. \(2014\). New insights into discretization effects in cellular automata models for pedestrian evacuation. *Physica A: Statistical Mechanics and Its Applications*, *400*, 1–11. 

https://doi.org/10.1016/j.physa.2014.01.001 

Guo, Y., Essa, M., Sayed, T., Haque, Md. M., & Washington, S. \(2019\). A comparison between simulated and field-measured conflicts for safety assessment of signalized intersections in Australia. *Transportation Research Part C: Emerging Technologies*, *101*, 96–110. 

https://doi.org/10.1016/j.trc.2019.02.009 

Hacohen, S., Shvalb, N., & Shoval, S. \(2018\). Dynamic model for pedestrian crossing in congested traffic based on probabilistic navigation function. *Transportation Research* *Part C: Emerging Technologies*, *86*, 78–96. https://doi.org/10.1016/j.trc.2017.10.024 

95 





Hamidun, R., Shabadin, A., Roslan, A., Sarani, R., & Johari, N. M. \(2021\). Analysis of Pedestrians’ Jaywalking at the Signalized Midblock in Kuala Lumpur, Malaysia. 

*International Journal of Road Safety*, *2*\(1\), Article 1. 

Harwood, D. W., Bauer, K. M., Richard, K. R., Gilmore, D. K., Graham, J. L., Potts, I. B., Torbic, D. J., & Hauer, E. \(2008\). Pedestrian Safety Prediction Methodology. *NCHRP *

*Web-Only Document*, *129: Phase III*, Article NCHRP Project 17-26. 

https://trid.trb.org/View/864886 

Hauer, E., Bonneson, J. A., Council, F., Srinivasan, R., & Zegeer, C. \(2012\). Crash Modification Factors: Foundational Issues. *Transportation Research Record*, *2279*\(1\), 67–74. 

https://doi.org/10.3141/2279-08 

Hayward, J. C. \(1972\). NEAR-MISS DETERMINATION THROUGH USE OF A SCALE OF 

DANGER. *Highway Research Record*, *384*. https://trid.trb.org/View/115323 

Helbing, D., Farkas, I., & Vicsek, T. \(2000\). Simulating Dynamical Features of Escape Panic. 

*Nature*, *407*\(6803\), 487–490. https://doi.org/10.1038/35035023 

Helbing, D., & Molnár, P. \(1995\). Social force model for pedestrian dynamics. *Physical Review* *E*, *51*\(5\), 4282–4286. https://doi.org/10.1103/PhysRevE.51.4282 

Hsu, Y.-C., Gopalswamy, S., Saripalli, S., & Shell, D. A. \(2018\). An MDP Model of Vehicle-Pedestrian Interaction at an Unsignalized Intersection. *2018 IEEE 88th Vehicular* *Technology Conference \(VTC-Fall\)*, 1–6. https://doi.org/10.1109/VTCFall.2018.8690813 

Huang, F., Liu, P., Yu, H., & Wang, W. \(2013\). Identifying if VISSIM simulation model and SSAM provide reasonable estimates for field measured traffic conflicts at signalized intersections. *Accident Analysis & Prevention*, *50*, 1014–1024. 

https://doi.org/10.1016/j.aap.2012.08.018 

96 





Hussein, M., & Sayed, T. \(2019\). Validation of an agent-based microscopic pedestrian simulation model in a crowded pedestrian walking environment. *Transportation Planning* *and Technology*, *42*\(1\), 1–22. https://doi.org/10.1080/03081060.2018.1541279 

Hydén, C. \(1987\). The development of a method for traffic safety evaluation: The Swedish Traffic Conflicts Technique. *Lund University*. 

Islam, Md. R., & Horio, K. \(2024\). Identification of Human Activity by Utilizing YOLOv5s Approaches. *2024 IEEE 3rd International Conference on Computing and Machine* *Intelligence \(ICMI\)*, 1–7. https://doi.org/10.1109/ICMI60790.2024.10586161 

Islam, Z., Abdel-Aty, M., Goswamy, A., Abdelraouf, A., & Zheng, O. \(2022\). *Modelling the* *Relationship Between Post Encroachment Time and Signal Timings Using UAV Video* *data* \(No. arXiv:2210.05044\). arXiv. https://doi.org/10.48550/arXiv.2210.05044 

Ismail, K., Sayed, T., & Saunier, N. \(2010\). Automated Analysis of Pedestrian–Vehicle Conflicts: Context for Before-and-After Studies. *Transportation Research Record*, *2198*\(1\), 52–64. https://doi.org/10.3141/2198-07 

Ismail, K., Sayed, T., & Saunier, N. \(2013\). *Camera Calibration for Urban Traffic Scenes:* *Practical Issues and a Robust Approach*. 

https://www.researchgate.net/publication/228670126\_Camera\_Calibration\_for\_Urban\_Tr affic\_Scenes\_Practical\_Issues\_and\_a\_Robust\_Approach 

Jason, L. A., & Liotta, R. \(1982\). Pedestrian Jaywalking Under Facilitating and Nonfacilitating Conditions. *Journal of Applied Behavior Analysis*, *15*\(3\), 469–473. 

https://doi.org/10.1901/jaba.1982.15-469 

Jennings, N. R. \(2000\). On agent-based software engineering. *Artificial Intelligence*, *117*\(2\), 277–296. https://doi.org/10.1016/S0004-3702\(99\)00107-1 

97 





Jin, B. \(2024\). Unlocking the Potential of Raw Images for Object Detection with YOLOv8 and BOT-SORT Techniques. *2024 5th International Conference on Machine Learning and* *Computer Application \(ICMLCA\)*, 252–257. 

https://doi.org/10.1109/ICMLCA63499.2024.10754493 

Johnsson, C., Laureshyn, A., & D’Agostino, C. \(2021\). Validation of surrogate measures of safety with a focus on bicyclist–motor vehicle interactions. *Accident Analysis &* *Prevention*, *153*. https://doi.org/10.1016/j.aap.2021.106037 

Karamouzas, I., Heil, P., van Beek, P., & Overmars, M. H. \(2009\). A Predictive Collision Avoidance Model for Pedestrian Simulation. In A. Egges, R. Geraerts, & M. Overmars \(Eds.\), *Motion in Games* \(pp. 41–52\). Springer. https://doi.org/10.1007/978-3-642-10347-6\_4 

Lanzaro, G., Sayed, T., & Fu, C. \(2023\). A comparison of pedestrian behavior in interactions with autonomous and human-driven vehicles: An extreme value theory approach. 

*Transportation Research Part F: Traffic Psychology and Behaviour*, *99*, 1–18. 

https://doi.org/10.1016/j.trf.2023.10.006 

Laureshyn, A., & Varhelyi, A. \(2018\). The Swedish Traffic Conflict Technique—Observer’s manual. *Lund University*. 

https://lucris.lub.lu.se/ws/files/51195704/TCT\_Manual\_2018.pdf Legal Information Institute. \(2021\). *Jaywalking*. Cornell Law School. 

https://www.law.cornell.edu/wex/jaywalking 

Leur, P. de, & Sayed, T. \(2001\). Using claims prediction model for road safety evaluation. 

*Canadian Journal of Civil Engineering*, *28*\(5\), 804–812. https://doi.org/10.1139/l01-046 

98 





Lewyn, M. \(2017\). The Criminalization of Walking. *University of Illinois Law Review*, *2017*, 1167. 

Li, B. \(2013\). A model of pedestrians’ intended waiting times for street crossings at signalized intersections. *Transportation Research Part B: Methodological*, *51*, 17–28. 

https://doi.org/10.1016/j.trb.2013.02.002 

Li, D., Li, Y., & Yuan, X. \(2014\). Effect of situational factors on pedestrian intention to jaywalk. 

*17th International IEEE Conference on Intelligent Transportation Systems \(ITSC\)*, 1770–

1774. https://doi.org/10.1109/ITSC.2014.6957949 

Li, T., Kothuri, S., Keeling, K., Yang, X., & Chowdhury, F. \(2023\). Pedestrian Behavior Study to Advance Pedestrian Safety in Smart Transportation Systems Using Innovative LiDAR 

Sensors. *TREC Final Reports*. https://doi.org/10.15760/trec.286 

Li, T., Li, Z., Mu, Y., & Su, J. \(2023\). Pedestrian multi-object tracking based on YOLOv7 and BoT-SORT. *Third International Conference on Computer Vision and Pattern Analysis* *\(ICCPA 2023\)*, *12754*, 369–374. https://doi.org/10.1117/12.2684256 

Lin, X., Beling, P. A., & Cogill, R. \(2014\). *Comparison of Multi-agent and Single-agent Inverse* *Learning on a Simulated Soccer Example* \(No. arXiv:1403.6822\). arXiv. 

https://doi.org/10.48550/arXiv.1403.6822 

Littman, M. L. \(1994\). Markov games as a framework for multi-agent reinforcement learning. In *Machine Learning Proceedings 1994* \(pp. 157–163\). Elsevier. 

https://doi.org/10.1016/B978-1-55860-335-6.50027-1 

Liu, C., Tao, Y., Liang, J., Li, K., & Chen, Y. \(2018\). Object Detection Based on YOLO 

Network. *2018 IEEE 4th Information Technology and Mechatronics Engineering* *Conference \(ITOEC\)*, 799–803. https://doi.org/10.1109/ITOEC.2018.8740604 

99 





Liu, T., Yang, X., Wang, Q., Zhou, M., & Xia, S. \(2020\). A Fuzzy-Theory-Based Cellular Automata Model for Pedestrian Evacuation From a Multiple-Exit Room. *IEEE Access*, *8*, 106334–106345. IEEE Access. https://doi.org/10.1109/ACCESS.2020.3000606 

Lu, L., Ren, G., Wang, W., Chan, C.-Y., & Wang, J. \(2016\). A cellular automaton simulation model for pedestrian and vehicle interaction behaviors at unsignalized mid-block crosswalks. *Accident Analysis & Prevention*, *95*, 425–437. 

https://doi.org/10.1016/j.aap.2016.04.014 

Macal, C. M., & North, M. J. \(2005\). Tutorial on agent-based modeling and simulation. 

*Proceedings of the Winter Simulation Conference, 2005. *, 14 pp.-. 

https://doi.org/10.1109/WSC.2005.1574234 

Mahmud, S. M. S., Ferreira, L., Hoque, Md. S., & Tavassoli, A. \(2019\). Micro-simulation modelling for traffic safety: A review and potential application to heterogeneous traffic environment. *IATSS Research*, *43*\(1\), 27–36. https://doi.org/10.1016/j.iatssr.2018.07.002 

Martinez-Gil, F., Lozano, M., García-Fernández, I., Romero, P., Serra, D., & Sebastián, R. 

\(2020\). Using Inverse Reinforcement Learning with Real Trajectories to Get More Trustworthy Pedestrian Simulations. *Mathematics*, *8*\(9\), Article 9. 

https://doi.org/10.3390/math8091479 

McKelvey, R. D., & Palfrey, T. R. \(1995\). Quantal Response Equilibria for Normal Form Games. *Games and Economic Behavior*, *10*\(1\), 6–38. 

https://doi.org/10.1006/game.1995.1023 

Minderhoud, M. M., & Bovy, P. H. L. \(2001\). Extended time-to-collision measures for road traffic safety assessment. *Accident Analysis & Prevention*, *33*\(1\), 89–97. 

https://doi.org/10.1016/S0001-4575\(00\)00019-1 

100 





Moussaïd, M., Perozo, N., Garnier, S., Helbing, D., & Theraulaz, G. \(2010\). The Walking Behaviour of Pedestrian Social Groups and Its Impact on Crowd Dynamics. *PLOS ONE*, *5*\(4\), e10047. https://doi.org/10.1371/journal.pone.0010047 

Moyano Dı́az, E. \(2002\). Theory of planned behavior and pedestrians’ intentions to violate traffic regulations. *Transportation Research Part F: Traffic Psychology and Behaviour*, *5*\(3\), 169–175. https://doi.org/10.1016/S1369-8478\(02\)00015-3 

Mullen, B., Copper, C., & E. Driskell, J. \(1990\). Jaywalking as a Function of Model Behavior. 

*Personality and Social Psychology Bulletin*, *16*\(16\), 320–330. 

https://doi.org/10.1177/0146167290162012 

Nasernejad, P., Sayed, T., & Alsaleh, R. \(2021a\). Modeling pedestrian behavior in pedestrian-vehicle near misses: A continuous Gaussian Process Inverse Reinforcement Learning \(GP-IRL\) approach. *Accident; Analysis and Prevention*, *161*, 106355. 

https://doi.org/10.1016/j.aap.2021.106355 

Nasernejad, P., Sayed, T., & Alsaleh, R. \(2021b\). Modeling pedestrian behavior in pedestrian-vehicle near misses: A continuous Gaussian Process Inverse Reinforcement Learning \(GP-IRL\) approach. *Accident Analysis & Prevention*, *161*, 106355. 

https://doi.org/10.1016/j.aap.2021.106355 

Nasernejad, P., Sayed, T., & Alsaleh, R. \(2023\). Multiagent modeling of pedestrian-vehicle conflicts using Adversarial Inverse Reinforcement Learning. *Transportmetrica A:* *Transport Science*, *19*\(3\), 2061081. https://doi.org/10.1080/23249935.2022.2061081 

Nash, J. \(1951\). Non-Cooperative Games. *Annals of Mathematics*, *54*\(2\), 286–295. 

https://doi.org/10.2307/1969529 

101 





Ng, A. Y., & Russell, S. \(2000\). *Algorithms for Inverse Reinforcement Learning*. 

https://www.researchgate.net/publication/2622278\_Algorithms\_for\_Inverse\_Reinforcem ent\_Learning 

Nowe, A., Vrancx, P., & De Hauwere, Y.-M. \(2012\). Game theory and multi-agent reinforcement learning. In *Reinforcement Learning. * \(pp. 441–470\). Springer. 

Parisi, D. R., & Dorso, C. O. \(2005\). Microscopic dynamics of pedestrian evacuation. *Physica A:* *Statistical Mechanics and Its Applications*, *354*, 606–618. 

Pascucci, F., Rinke, N., Schiermeyer, C., Berkhahn, V., & Friedrich, B. \(2017\). *A discrete choice* *model for solving conflict situations between pedestrians and vehicles in shared space* \(No. arXiv:1709.09412\). arXiv. https://doi.org/10.48550/arXiv.1709.09412 

Perkins, S. R., & Harris, J. L. \(1968\). Traffic conflict characteristics-accident potential at intersections. *Highway Research Record*, *225*. https://trid.trb.org/View/1310479 

Puterman, M. L. \(1990\). Chapter 8 Markov decision processes. In *Handbooks in Operations* *Research and Management Science* \(Vol. 2, pp. 331–434\). Elsevier. 

https://doi.org/10.1016/S0927-0507\(05\)80172-0 

Rad, S. R., Hagenzieker, M., & Correia, G. H. de A. \(2020\). Pedestrians’ road crossing behaviour in front of automated vehicles: Results from a pedestrian simulation experiment using agent-based modelling. *Transportation Research Part F: Traffic* *Psychology and Behaviour*, *69*, 101–119. https://doi.org/10.1016/j.trf.2020.01.014 

Raghuram Kadali, B., Rathi, N., & Perumal, V. \(2014\). Evaluation of pedestrian mid-block road crossing behaviour using artificial neural network. *Journal of Traffic and Transportation* *Engineering \(English Edition\)*, *1*\(2\), 111–119. https://doi.org/10.1016/S2095-7564\(15\)30095-7 

102 





Richl, L., & Sayed, T. \(2006\). Evaluating the Safety Risk of Narrow Medians Using Reliability Analysis. *Journal of Transportation Engineering*, *132*\(5\), 366–375. 

https://doi.org/10.1061/\(ASCE\)0733-947X\(2006\)132:5\(366\) 

RSBC. \(1996\). *Motor Vehicle Act*. 

https://www.bclaws.gov.bc.ca/civix/document/id/complete/statreg/96318\_05 

Russo, B. J., James, E., Aguilar, C. Y., & Smaglik, E. J. \(2018\). Pedestrian behavior at signalized intersection crosswalks: Observational study of factors associated with distracted walking, pedestrian violations, and walking speed. *Transportation Research Record*, *2672*\(35\), 1–12. https://doi.org/10.1177/0361198118759949 

Sacchi, E., & Sayed, T. \(2016\). Conflict-Based Safety Performance Functions for Predicting Traffic Collisions by Type. *Transportation Research Record*, *2583*\(1\), 50–55. 

https://doi.org/10.3141/2583-07 

Saneinejad, S., & Lo, J. \(2015\). Leading Pedestrian Interval: Assessment and Implementation Guidelines. *Transportation Research Board*, *2519*. https://doi.org/10.3141/2519-10 

Saunier, N., & Sayed, T. \(2006\). A feature-based tracking algorithm for vehicles in intersections. 

*The 3rd Canadian Conference on Computer and Robot Vision \(CRV’06\)*, 59–59. 

https://doi.org/10.1109/CRV.2006.3 

Saunier, N., & Sayed, T. \(2007\). Automated Analysis of Road Safety with Video Data. 

*Transportation Research Record*, *2019*\(1\), 57–64. https://doi.org/10.3141/2019-08 

Savitzky, A., & Golay, M. J. \(1964\). Smoothing and differentiation of data by simplified least squares procedures. *Analytical Chemistry*, *36*\(8\), 1627–1639. 

103 





Sayed, T., Zaki, M. H., & Autey, J. \(2013\). Automated safety diagnosis of vehicle–bicycle interactions using computer vision analysis. *Safety Science*, *59*, 163–172. 

https://doi.org/10.1016/j.ssci.2013.05.009 

Sayed, T., & Zein, S. \(1999\). Traffic conflict standards for intersections. *Transportation* *Planning and Technology*, *22*\(4\), 309–323. https://doi.org/10.1080/03081069908717634 

Sisiopiku, V. P., & Akin, D. \(2003\). Pedestrian behaviors at and perceptions towards various pedestrian facilities: An examination based on observation and survey data. 

*Transportation Research Part F: Traffic Psychology and Behaviour*, *6*\(4\), 249–274. 

https://doi.org/10.1016/j.trf.2003.06.001 

Song, J., Ren, H., Sadigh, D., & Ermon, S. \(2018\). Multi-Agent Generative Adversarial Imitation Learning. *Advances in Neural Information Processing Systems*, *31*. 

https://papers.nips.cc/paper\_files/paper/2018/hash/240c945bb72980130446fc2b40fbb8e0

-Abstract.html 

Svensson, Å. \(1998\). A method for analysing the traffic process in a safety perspective 

\[Thesis/docmono, Lund University\]. In *Bulletin / University of Lund, Lund Institute of* *Technology, Department of Traffic Planning and Engineering* \(Vol. 166\). 

http://lup.lub.lu.se/record/18638 

Tang, J., Ye, C., Zhou, X., & Xu, L. \(2024\). YOLO-Fusion and Internet of Things: Advancing object detection in smart transportation. *Alexandria Engineering Journal*, *107*, 1–12. 

https://doi.org/10.1016/j.aej.2024.09.012 

Tarko, A. P., & Songchitruksa, P. \(2005\). Estimating the frequency of crashes as extreme traffic events. *84th Annual Meeting of the Transportation Research Board. * 

104 





Tiwari, G., Bangdiwala, S., Saraswat, A., & Gaurav, S. \(2007\). Survival analysis: Pedestrian risk exposure at signalized intersections. *Transportation Research Part F: Traffic Psychology* *and Behaviour*, *10*\(2\), 77–89. https://doi.org/10.1016/j.trf.2006.06.002 

Toronto, C. of. \(2021, October 29\). *Rules for crossing the street—Jaywalking—Pedestrian traffic* *signals* \(Toronto, Ontario, Canada\). City of Toronto; City of Toronto. 

https://www.toronto.ca/home/311-toronto-at-your-service/find-service-information/article/ 

Ulfarsson, G. F., Kim, S., & Booth, K. M. \(2010\). Analyzing fault in pedestrian-motor vehicle crashes in North Carolina. *Accident; Analysis and Prevention*, *42*\(6\), 1805–1813. 

https://doi.org/10.1016/j.aap.2010.05.001 

UNECE. \(2021\). *Second Decade of Action | UNECE*. https://unece.org/second-decade-action Vasudevan, V., Agarwala, R., & Tiwari, A. \(2022\). LiDAR-Based Vehicle–Pedestrian Interaction Study on Midblock Crossing Using Trajectory-Based Modified Post-Encroachment Time. *Transportation Research Record*, *2676*\(7\), 837–847. 

https://doi.org/10.1177/03611981221083295 

Waizman, G., Shoval, S., & Benenson, I. \(2015\). Micro-simulation model for assessing the risk of vehicle-pedestrian road accidents. *Journal of Intelligent Transportation Systems*, *19*\(1\), 63–77. 

WHO. \(2023a\). *Pedestrian safety: A road safety manual for decision-makers and practitioners,* *2nd edition*. World Health Organization. 

WHO. \(2023b\). *Road traffic injuries*. World Health Organization. https://www.who.int/news-room/fact-sheets/detail/road-traffic-injuries 

105 





Wojke, N., Bewley, A., & Paulus, D. \(2017\). *Simple Online and Realtime Tracking with a Deep* *Association Metric* \(No. arXiv:1703.07402\). arXiv. 

https://doi.org/10.48550/arXiv.1703.07402 

World Health Organization. \(2018\). *Global status report on road safety 2018*. World Health Organization. 

Xie, D. F., Gao, Z. Y., Zhao, X. M., & Wang, D. Z. W. \(2012\). Cellular Automaton Modeling of the Interaction between Vehicles and Pedestrians at Signalized Crosswalk. *Journal of* *Transportation Engineering*, *138*\(12\). https://doi.org/10.1061/\(ASCE\)TE.1943-5436.0000462 

XIE, S., Wong, S. C., Ng, T. M., & Lam, W. H. K. L. \(2017\). \(PDF\) Pedestrian Crossing Behavior at Signalized Crosswalks. *Journal of Transportation Engineering Part A* *Systems*, *143*\(8\). https://doi.org/10.1061/JTEPBS.0000055 

Xin, W., Hourdos, J., & Michalopoulos, P. \(2008\). *Enhanced Micro-Simulation Models for* *Accurate Safety Assessment of Traffic Management ITS Solutions | Center for* *Transportation Studies*. https://www.cts.umn.edu/publications/report/enhanced-microsimulation-models-for-accurate-safety-assessment-of-traffic-management-its-solutions?utm\_source=chatgpt.com 

Ye, J., Chen, X., Yang, C., & Wu, J. \(2008\). Walking Behavior and Pedestrian Flow Characteristics for Different Types of Walking Facilities. *Transportation Research* *Record*, *2048*\(1\), 43–51. https://doi.org/10.3141/2048-06 

Yu, L., Song, J., & Ermon, S. \(2019\). *Multi-Agent Adversarial Inverse Reinforcement Learning* \(No. 1907.13220v1; Issue arXiv:1907.13220v1\). 

106 





Zaki, M. H., & Sayed, T. \(2013\). A framework for automated road-users classification using movement trajectories. *Transportation Research Part C: Emerging Technologies*, *33*, 50–

73. https://doi.org/10.1016/j.trc.2013.04.007 

Zaki, M. H., Sayed, T., Ismail, K., & Alrukaibi, F. \(2012\). Use of Computer Vision to Identify Pedestrians’ Nonconforming Behavior at Urban Intersections. *Transportation Research* *Record*, *2279*\(1\), 54–64. https://doi.org/10.3141/2279-07 

Zaki, M. H., Sayed, T., & Wang, X. \(2016\). Computer vision approach for the classification of bike type \(motorized versus non-motorized\) during busy traffic in the city of Shanghai. 

*Journal of Advanced Transportation*, *50*\(3\), 348–362. https://doi.org/10.1002/atr.1327 

Zeng, W., Chen, P., Nakamura, H., & Iryo-Asano, M. \(2014\). Application of social force model to pedestrian behavior analysis at signalized crosswalk. *Transportation Research Part C:* *Emerging Technologies*, *40*, 143–159. https://doi.org/10.1016/j.trc.2014.01.007 

Zhang, Z., Li, H., & Ren, G. \(2023\). Investigating jaywalker crossing risks from the sequential-conflict perspective: A grouped random parameters generalized ordered probit model. 

*Accident Analysis & Prevention*, *189*, 107145. https://doi.org/10.1016/j.aap.2023.107145 

Zheng, L., Ismail, K., & Meng, X. \(2014\). Traffic conflict techniques for road safety analysis: Open questions and some insights. *Canadian Journal of Civil Engineering*, *41*\(7\), 633–

641. https://doi.org/10.1139/cjce-2013-0558 

Zheng, L., Sayed, T., & Mannering, F. \(2021\). Modeling traffic conflicts for use in road safety analysis: A review of analytic methods and future directions. *Analytic Methods in* *Accident Research*, *29*, 100142. https://doi.org/10.1016/j.amar.2020.100142 

107 





Zhou, Z., Zhou, Y., Yongneng, X., & Pu, Z. \(2019\). Simulation of pedestrian behavior during the flashing green signal using a modified social force model. *Transportmetrica A Transport* *Science*, *15*\(2\), 1019–1040. https://doi.org/10.1080/23249935.2018.1559895 

Zhou, Z.-P., Liu, Y.-S., Wang, W., & Zhang, Y. \(2013\). Multinomial Logit Model of Pedestrian Crossing Behaviors at Signalized Intersections. *Discrete Dynamics in Nature and Society*, *2013*\(1\), 172726. https://doi.org/10.1155/2013/172726 

Zhu, H., Almukdad, A., Iryo-Asano, M., Alhajyaseen, W. K. M., Nakamura, H., & Zhang, X. 

\(2021\). A novel agent-based framework for evaluating pedestrian safety at unsignalized mid-block crosswalks. *Accident Analysis & Prevention*, *159*, 106288. 

https://doi.org/10.1016/j.aap.2021.106288 

Ziebart, B. D., Maas, A., Bagnell, J. A., & Dey, A. K. \(2008\). *Maximum Entropy Inverse* *Reinforcement Learning*. 





108



