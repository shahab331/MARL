**Traffic Injury Prevention**

**ISSN: \(Print\) \(Online\) Journal homepage: www.tandfonline.com/journals/gcpi20**

**Predicting pedestrian-vehicle interaction severity at**

**unsignalized intersections**

**Kaliprasana Muduli & Indrajit Ghosh**

**To cite this article:** Kaliprasana Muduli & Indrajit Ghosh \(15 Oct 2024\): Predicting pedestrian-vehicle interaction severity at unsignalized intersections, Traffic Injury Prevention, DOI:

10.1080/15389588.2024.2404713

**To link to this article: **https://doi.org/10.1080/15389588.2024.2404713

View supplementary material 

Published online: 15 Oct 2024. 

Submit your article to this journal 

Article views: 325

View related articles 

View Crossmark data

Ful Terms & Conditions of access and use can be found at

https://www.tandfonline.com/action/journalInformation?journalCode=gcpi20

Traffic injury PrevenTion

https://doi.org/10.1080/15389588.2024.2404713

**Predicting pedestrian-vehicle interaction severity at unsignalized intersections** Kaliprasana Muduli and Indrajit Ghosh 

Department of civil engineering, indian institute of Technology \(iiT\) roorkee, roorkee, india **ABSTRACT**

**ARTICLE HISTORY**

**Objectives: **This study aims to develop and validate a novel deep-learning model that predicts the received 24 May 2024

severity of pedestrian-vehicle interactions at unsignalized intersections, distinctively integrating accepted 11 September 2024

Transformer-based models with Multilayer Perceptrons \(MLP\). This approach leverages advanced **KEYWORDS**

feature analysis capabilities, offering a more direct and interpretable method than traditional Pedestrian safety; traffic 

models. 

modeling; deep learning; 

**Methods: **High-resolution optical cameras recorded detailed pedestrian and vehicle movements at unsignalized intersections; 

study sites, with data processed to extract trajectories and convert them into real-world coordinates variable importance

*via* precise georeferencing. Trained observers categorized interactions into safe passage, critical event, and conflict based on movement patterns, speeds, and accelerations. Fleiss Kappa statistic measured inter-rater agreement to ensure evaluator consistency. This study introduces a novel deep-learning model combining Transformer-based time series data capabilities with the classification strengths of a Multilayer Perceptron \(MLP\). Unlike traditional models, this approach focuses on feature analysis for greater interpretability. The model, trained on dynamic input variables from trajectory data, employs attention mechanisms to evaluate the significance of each input variable, offering deeper insights into factors influencing interaction severity. 

**Results: **The model demonstrated high performance across different severity categories: safe interactions achieved a precision of 0.78, recall of 0.91, and F1-score of 0.84. In more severe categories like critical events and conflicts, precision and recall were even higher. Overall accuracy stood at 0.87, with both macro and weighted averages for precision, recall, and F1-score also at 0.87. The variable importance analysis, using attention scores from the proposed transformer model, identified ‘Vehicle Speed’ as the most significant input variable positively influencing severity. 

Conversely, ‘Approaching Angle’ and ‘Vehicle Distance from Conflict Point’ negatively impacted severity. Other significant factors included ‘Type of Vehicle’, ‘Pedestrian Speed’, and ‘Pedestrian Yaw Rate’, highlighting the complex interplay of behavioral and environmental factors in pedestrian-vehicle interactions. 

**Conclusions: **This study introduces a deep-learning model that effectively predicts the severity of pedestrian-vehicle interactions at crosswalks, utilizing a Transformer-MLP hybrid architecture with high precision and recall across severity categories. Key factors influencing severity were identified, paving the way for further enhancements in real-time analysis and broader safety assessments in urban settings. 

**Introduction**

These concerning statistics highlight the necessity for 

innovative solutions such as predictive models for 

Road traffic crashes continue to be a major global concern, pedestrian-vehicle interactions. By leveraging data on the causing significant mortality and morbidity among pedestri- dynamics of these interactions, such models can significantly ans, motorcyclists, and cyclists, collectively known as vulner- enhance our ability to predict and mitigate the severity of able road users \(VRUs\). Recent global data indicate that these encounters. Advanced predictive models facilitate the these groups constitute over half of all traffic-related fatali- development of integrated pedestrian safety systems that utities \(WHO 2023\). In India, the situation is particularly lize Infrastructure to Vehicle \(I2V\) and Infrastructure to alarming, with an annual average of 150,000 fatalities, many Pedestrian \(I2P\) technologies. Through smartphones or occurring at junctions devoid of traffic control measures wearable devices, these systems offer real-time insights into \(MORTH 2022\). Research indicates that many pedestrian potential hazards, significantly enhancing pedestrian situa-fatalities in India happen at uncontrolled crossing points tional awareness. Historical y, studies on pedestrian road- 

\(Bansal et al. 2018; Mukherjee and Mitra 2019\), underscor- crossing safety have fallen into two categories: crash-based, ing the urgent need for effective safety interventions. 

which analyze previous road crashes to predict future events, 

**CONTACT **indrajit Ghosh  indrafce@iitr.ac.in, indrajit.ghosh@ce.iitr.ac.in 

Transportation engineering Group, Department of civil engineering, indian institute of Technology \(iiT\) roorkee, roorkee 247667, uttarakhand, india. 

associate editor alessandro calvi oversaw the review of this article. 

Supplemental data for this article can be accessed online at https://doi.org/10.1080/15389588.2024.2404713. 

© 2024 Taylor & francis Group, LLc

2

K. MUDULI AND I. GHOSH

and conflict-based, which utilize data from non-crash inter- traffic conflict indicators like PET or TTC to evaluate the pre-actions to predict and measure potential conflicts \(Shahdah dicted severity of interactions. However, as Golchoubian et al. 

et al. 2014; Formosa et al. 2020; Mohammadian et al. 2021; \(2023\) noted that trajectory prediction models in mixed traffic Nie et al. 2021\). Conflict-based studies define traffic con- conditions can accumulate significant errors over time, leading flicts as situations where the paths of road users intersect in to unreliable outcomes. To address the complexities and limita-such a way that could lead to a crash unless corrective tions of traditional predictive models, this study introduces a actions are taken \(Hydén and Linderholm 1984\), providing novel approach utilizing a Transformer model architecture a proactive means to assess traffic safety. 

known for its exceptional ability to handle time-series data. 

Real-time prediction of crash probability significantly Unlike traditional methods that often rely on historical data to enhances traffic safety by allowing proactive measures to be make linear predictions, our Transformer-based model dynam-implemented before accidents occur. Studies have shown that ical y incorporates multiple input features, such as speed, direc-machine learning models such as Support Vector Machine tion, and environmental context, in real-time. This allows the \(SVM\) and Multilayer Perceptron \(MLP\) can effectively pre- model to adapt to changing conditions and more accurately dict crash occurrences by analyzing real-time traffic data predict the interaction severities. The architecture leverages the \(Elamrani Abou Elassad et al. 2020\). To improve pedestrian Transformer’s multi-headed attention mechanism, which safety, Conflict Warning Systems, including sophisticated focuses on different aspects of the traffic scenario at various infrastructure-based systems and Advanced Driver Assistance time intervals, providing a nuanced understanding of the Systems \(ADAS\), are crucial. These systems predict the sever- dynamic interactions between pedestrians and vehicles. This ity of pedestrian-vehicle interactions, enabling them to alert approach enhances the accuracy of predicting immediate risks road users about potential high-risk scenarios that could esca- and significantly improves the interpretability of the model’s late into road crashes \(Rasouli and Tsotsos 2020\). ADAS, for decisions. By directly analyzing critical features without the instance, uses Surrogate Safety Measures \(SSMs\) such as Time need to predict extended future trajectories, our model reduces to Collision \(TTC\) to warn drivers of impending conflicts computational overhead and minimizes the accumulation of when, e.g., TTC fal s below a certain threshold \(Han et al. prediction errors over multiple time steps. The integration of 

2014\). TTC is calculated based on the assumption that both this advanced modeling technique represents a significant leap pedestrian and vehicle maintain constant speeds on their cur- forward in real-time traffic safety analysis, offering a robust rent paths \(Hayward 1972\). However, this method often fails tool for developing proactive pedestrian safety systems that to account for the dynamic nature of road interactions, where can seamlessly integrate with modern traffic management users frequently adjust their speeds or directions in response technologies. 

to their immediate environment. This limitation can lead to 

The objective of this study is to develop and validate an 

inaccurate risk assessments, either overestimating or underes- interpretable machine-learning model designed to predict timating the actual threat of a conflict \(Li et al. 2022\). Post the severity of pedestrian-vehicle interactions at unsignalized Encroachment Time \(PET\), another traditional indicator, intersections, with the ultimate aim of deploying this model evaluates the time difference between when a pedestrian and to provide timely warnings to road users so that pedestrian a vehicle occupy the same space \(Cooper 1984\). While PET crashes can be avoided. This study addresses the complexi-offers insights into past interactions, it cannot predict or ties and limitations of traditional predictive models by intro-assess the potential severity of future conflicts in real-time. 

ducing a novel deep learning approach. The proposed model 

Recent advancements in traffic safety research have utilizes a feature-based transformer architecture that dynam-explored sophisticated trajectory prediction techniques to ical y incorporates real-time data inputs, allowing for instan-enhance pedestrian safety. For instance, Selmoune et al. taneous adjustments to changing conditions. Unlike 

\(2023\) developed a Collision Warning Service that integrates conventional methods, this model directly analyzes critical closed-circuit television systems \(CCTVs\), radar, and com- features without predicting extended future trajectories, puter vision to detect objects and predict their paths in effectively minimizing error accumulation over multiple time real-time using a perspective transformation method and the steps and reducing computational overhead. Additional y, Kalman filter. Similarly, Ezzati Amini et al. \(2022\) employed this study leverages attention scores generated by the model variables such as Minimum Future Relative Distance \(MD\), to dissect and highlight the influence of various features on Time to Minimum Distance \(TMD\), and Conflicting Speed its predictions. This analysis offers vital insights into the pri-

\(CS\) to develop a logit model aimed at enhancing ADAS by mary factors that determine the severity of pedestrian-vehicle predicting the severity of pedestrian-vehicle interactions. Li interactions. By processing and prioritizing information in et al. \(2022\) proposed a probabilistic framework that employs real time, the model not only enhances the interpretability Gaussian process regression models for predicting the trajec- of its decisions but also establishes itself as a more reliable tories of both pedestrians and vehicles, integrating maneuver tool for proactive traffic safety management. 

probabilities for comprehensive risk analysis. This method 

proved to be more effective than traditional TTC in fore-

casting pedestrian-vehicle conflicts, offering a promising **Methods** solution for real-time safety management at intersections. 

***Data sources***

Predictive modeling in pedestrian safety involves multiple 

steps: predicting the future trajectories of pedestrians and vehi- To accurately predict the severity of interactions between cles, identifying potential conflict points, and then calculating pedestrians and vehicles, detailed data on the dynamics of 





TRAFFIC INjURY PReVeNTION

3

**Figure 1. ** information for selected study sites. 

their encounters is essential, including a substantial number 

of critical events to encompass the range of severity levels. 

For this purpose, two unsignalized intersections known for **Figure 2. ** Satellite imagery and mapped locations of the study sites. 

frequent pedestrian incidents were selected for data collection. 

Information about each location, such as the number of vehi-

cles and pedestrians, is detailed in Figure 1. A total of 8 h of video footage, 4 h from each intersection, was recorded to 

document the interaction dynamics. High-quality optical 

cameras were strategical y placed at each site to ensure com-

prehensive capture of road users’ movements. The selection 

of study sites was grounded in a comprehensive evaluation of 

historical crash data, high pedestrian activity, and consulta-

tions with local traffic management authorities. These inter-

sections were identified due to their significant incidence of 

pedestrian-vehicle interactions. The study periods were specif-

ical y chosen to encompass both morning and evening peak 

hours, which are well-known for high traffic volume and 

increased rates of pedestrian-vehicle interactions. This 

approach ensures that the data collected is representative of 

typical and critical conditions. The presence of local markets 

nearby adds to the complexity of traffic dynamics at these 

locations, contributing to varied pedestrian volumes through-

out the day. Additional y, data was collected in clear weather 

conditions to minimize the impact of environmental factors 

and the dynamics of pedestrian and vehicle interactions. Both 

sites feature a dual carriageway with two lanes in each direc-

tion, divided by a physical median and equipped with distinct 

lane markings and a zebra crossing. Figure 2 provides satellite imagery and detailed maps of the study sites. 

The data processing was carried out using DataFromSky 

\(DataFromSky 2024\), a commercial software, to extract 

high-resolution trajectories of road users from video footage **Figure 3. ** Manual georeferencing in DatafromSky, showing region of interest at each site. Its ability to analyze complex traffic scenarios \(roi\) delineation and coordinate mapping. 

from video data offers unparalleled detail, making 

“DataFromSky” particularly suitable for studies requiring ***Dataset preparation***

precise movement patterns and interaction analyses, and it 

has been validated in several peer-reviewed studies \(Adamec The trajectory data were analyzed to determine the PET for et al. 2020; Dhatbale et al. 2021\). Initial y, video frames were each pedestrian-vehicle pair with intersecting paths. PET mea-preprocessed on the DataFromSky web platform, generating sures the time interval between when one road user leaves a trajectory data in pixel units. Subsequently, the DataFromSky potential conflict zone and the next enters it \(Allen et al. 1978\).  

viewer application transformed these pixel coordinates into For detailed behavioral observation and interaction severity real-world coordinates through manual georeferencing. estimation, only interactions with a PET of less than 10 s were During this process, the Region of Interest \(ROI\) was considered. This threshold was used because a PET exceeding defined, and the geographical coordinates of five selected 10 s general y does not indicate a significant interaction. This points within the ROI were inputted. Figure 3 il ustrates the criterion is supported by the findings of Paul and Ghosh detailed steps of this transformation. The resulting \(2020\), who observed that the maximum PET values at differ-geo-registered trajectories were analyzed to extract the nec- ent unsignalized intersections across India ranged from 8 to essary input variables and traffic conflict indicators. 

11 s, reinforcing the practicality of the 10-second threshold. 

4

K. MUDULI AND I. GHOSH

***Behavior observation and interaction severity estimation***

observers to assess interaction severity by visual y perceiving 

In traffic safety research, methodologies that rely on observer the scene and utilizing well-informed quantitative knowledge ratings are essential for studying and understanding the about movement dynamics and traffic conflict indicators. 

dynamics of traffic conflicts and behaviors of road users. 

Earlier studies, such as those conducted by Van der Horst and **Classification schemes** Kraay \(1986\), Ni et al. \(2016\), and Kathuria and Vedagiri 

\(2020\), highlighted the efficacy of video observation in cap- ***Safe passage***

turing complex interactions between road users. These studies 

employed video observation techniques to classify Interactions where pedestrians and vehicles navigate the pedestrian-vehicle interactions into varying levels of severity. intersection without imminent risk, maintaining a comfort-Our study adopts a similar approach, utilizing the AI-enhanced able and safe distance and timing. No sudden maneuvers are platform DataFromSky Viewer for advanced analysis of tra- required, and the interaction is managed smoothly. These jectories, speeds, and acceleration profiles of all road users interactions can be associated with high PET values \(greater 

\(Figure B1, Supplementary material\). This tool provides a than 3 s\) indicating sufficient temporal separation, low or comprehensive means to assess interaction dynamics. 

moderate speeds \(up to 10 m/s\) with minimal or controlled 

With DataFromSky Viewer, observers can:

acceleration/deceleration \(below 1 m/s2\), and Smooth and 

predictable trajectories for both pedestrians and vehicles. 

• **Analyze Trajectories:** Enhance understanding of Observers perceive these interactions as calm and controlled, movement patterns and pinpoint potential conflict with clear intent from both parties. Some behavioral exam-points. 

ples relevant to safe passages include vehicle yielding, where 

• **Monitor Speed and Acceleration Profiles:** Evaluate the vehicle slows or stops well in advance to allow the changes in speed and acceleration to understand how pedestrian to cross; negotiated passage, involving slight road users react to potential conflicts. 

adjustments by both the pedestrian and vehicle for a smooth 

• **Estimate Severity:** Use detailed movement data to passage; and no action, where neither party changes speed inform assessments of interaction severity. 

nor path, yet the interaction concludes safely. 

Building on the established behaviors identified in the ***Critical event***

works of Ni et al. \(2016\) and Kathuria and Vedagiri \(2020\), our observers classified each interaction into one of three Interactions with moderate risk, where timely and appropriate severity levels: safe passage \(0\), critical event \(1\), and con- responses are required to avoid conflict. These interactions flict \(2\). The typical interactions observed as pedestrians and involve closer temporal and spatial proximity but are managed vehicles approach potential conflict zones include:

effectively. These interactions can be associated with moderate 

PET values \(between 1 and 3 s\) that indicate potential risk but 

1. **Pedestrian Withdrawal:** The pedestrian slows down, allow for evasive action, moderate speeds \(between 5 to 10 m/s\) stops, or moves away from the conflict zone, yielding with some level of acceleration or deceleration \(typical y to the approaching vehicle. 

between 1 and 3 m/s2\) indicating an active response, and some 

2. **Pedestrian Acceleration:** The pedestrian increases deviation from a smooth path, indicating adjustments made to their speed to cross before the vehicle arrives, indi- avoid conflict. Observers perceive these interactions as height-cating a judgment of safe passage. 

ened alertness and active maneuvers from either party to avoid 

3. **Path Change by Pedestrian:** The pedestrian alters their collision. Some behavioral examples relevant to critical events path, such as moving behind the vehicle, to avoid inter- include pedestrian withdrawal, where the pedestrian stops or action, reflecting adaptive safety maneuvers. 

moves back to yield to the vehicle; pedestrian acceleration, 

4. **Vehicle Yielding:** The vehicle slows or stops to allow where the pedestrian speeds up to cross before the vehicle the pedestrian to cross, showing recognition of the arrives; and path change by the pedestrian, where the pedes-pedestrian’s presence and avoiding potential conflict. 

trian alters their path to avoid the vehicle. 

5. **Vehicle Acceleration:** The vehicle speeds up to clear 

the conflict zone before the pedestrian enters, aiming ***Conflict***

to minimize interaction time. 

6. **Negotiated Passage:** Both the pedestrian and vehicle High-risk interactions involving near-misses, where evasive adjust their movements, achieving a safe passage through actions are either insufficient or too late. These represent the mutual adjustment without direct communication. 

most severe interactions. These interactions can be associated 

7. **No Action:** Neither party changes their speed or path, with low PET values \(typical y less than 1 s\), indicating very yet the interaction concludes safely without incident. 

close temporal proximity, high speeds \(greater than 10 m/s\) 

and/or abrupt acceleration or deceleration \(greater than 3 m/

These behavioral observations, which include subtle cues s2\), indicating emergency maneuvers, sharp deviations, and and context-specific behaviors, were combined with quanti- erratic paths indicating emergency responses. Observers per-tative values of speed, acceleration, trajectory plots for visu- ceive the interaction as chaotic and dangerous, often involv-alizing path changes, and PET values to gauge temporal ing sudden stops or swerves. Some behavioral examples closeness. This comprehensive approach empowered the relevant to conflicts include vehicle acceleration, where the 

TRAFFIC INjURY PReVeNTION

5

vehicle speeds up to clear the conflict zone before the pedes- **Table 1. ** input variables representing pedestrian dynamics. 

trian enters, and emergency maneuvers, involving sudden variable

Data type

feature description

braking or swerving by either party to avoid a collision. 

Pedestrian Speed

continuous variable Measured in meters per second 

To ensure consistency and reliability in our data, six 

\(m/s\)

trained observers evaluated a total of 4,315 interactions, Pedestrian Tangential continuous variable Measured in meters per second acceleration

squared \(m/s²\)

independently assigning severity levels based on the described Pedestrian Lateral continuous variable Measured in meters per second 

criteria. The observers were rigorously trained to utilize the 

acceleration

squared \(m/s²\)

DataFromSky Viewer and understand the categorization Pedestrian Distance continuous variable Measured in meters \(m\) from conflict Point

scheme. The robustness of our severity estimations was Pedestrian Direction continuous variable Measured in degrees enhanced through the use of Fleiss Kappa statistics \(Fleiss Pedestrian yaw rate continuous variable Measured in degrees per second \(°/s\)

1971\) to measure inter-rater agreement among the observers. 

This statistical method helped confirm the reliability of the **Table 2. ** input variables representing vehicle dynamics. 

observers’ assessments, ensuring that our findings were variable

Data type

feature description

based on consistent and accurate evaluations. 

vehicle Speed

continuous variable

Measured in meters per second 

\(m/s\)

vehicle Tangential 

continuous variable

Measured in meters per second 

***Assessment of observer agreement in severity level ***

acceleration

squared \(m/s²\)

***estimation***

vehicle Lateral 

continuous variable

Measured in meters per second 

In this study, we employed the Fleiss Kappa statistic \(Fleiss 

acceleration

squared \(m/s²\)

vehicle Distance from continuous variable

Measured in meters \(m\)

1971\) to assess the reliability of agreement among multiple conflict Point

observers evaluating the severity of pedestrian-vehicle interac- vehicle Direction continuous variable

Measured in degrees

tions. We organized the data into an n × k matrix, where vehicle yaw rate continuous variable

Measured in degrees per 

second \(°/s\)

*n* = 4,315 denotes the total observed events and *k* = 3 represents Type of vehicle nominal \(categorical\) Motorcycle \(0\), auto rickshaw 

the severity categories, with each matrix element reflecting the 

\(1\), car/Taxis/vans & LMv 

count of raters assigning each event to a category. We calcu-

\(2\), Bus \(3\), Truck/Lorry \(4\)

lated the proportional agreement among raters for each event 

and derived the overall mean proportional agreement \( *P*

**Table 3. ** input variables representing interaction dynamics. 

mean\). 

Expected agreement by chance \( *Pe*\) was determined from the variable Data type

feature description

rating proportions across categories. The Fleiss Kappa coeffi- approaching angle continuous variable

Measured in degrees

Longitudinal Distance

continuous variable

Measured in meters \(m\)

cient, calculated using Equation \(1\), yielded a value of 0.75. 

Lateral Distance

continuous variable

Measured in meters \(m\)

P

−P



κ = mean

e 

\(1\) Class 0 - Safe Passage, Class 1 - Critical Event, Class 2 - 

1− P

Conflict\), is used as the dependent variable. The prediction 

e

horizon of 2s was adopted, drawing on the findings of Nie 

This indicates a substantial level of inter-rater agreement et al. \(2021\), which says that pedestrians’ decision and execu-beyond what could occur by chance, validating the reliability tion times for avoidance actions range from 1.69 to 2.08 s. 

of our observational methodology as per the standards set 

To standardize the input data for the proposed model, 

by Landis and Koch \(1977\). 

the mode of the lengths of all extracted time series, calcu-

lated to be 60, has been determined as the standard length 

***Input variables***

for training. Interactions that yielded time series shorter 

To predict the severity of pedestrian-vehicle interactions and to than the mode were padded with zeros, whereas those implement a prototype system in an AI-enhanced pedestrian exceeding the mode were truncated to ensure uniformity. 

crossing, it is essential that the driver and the pedestrian receive This methodological rigor ensures that the model is trained an advance warning for critical interactions θ time units before on consistently formatted data, enhancing its predictive they occur. Considering the reaction time of drivers and pedes- accuracy and reliability in real-world applications. 

trians, θ was established as 2 s. The trajectories of interacting 

Position coordinates from the trajectory data, given in 

road users 2s before reaching their minimum separation dis- latitude and longitude, necessitated the use of the Haversine tance were analyzed to extract the necessary input variables, formula to calculate distances essential for determining input which represent Pedestrian Dynamics, Vehicle Dynamics, and variables such as approach angle, longitudinal and lateral Interaction Dynamics, presented in Table 1, Table 2,  and distances, speed, and acceleration. The Haversine distance 

Table 3, respectively. For training the proposed machine learn- \(d\) between two points is calculated using the following for-ing model Pedestrian-Vehicle Interaction Severity \(Ordinal: mula as presented in Equation \(1\). 









2

2

lat



2 − lat1 



 lon2− lon1



sin

cos lat1

cos lat







 \+

\(

\)× \( 2\)×sin









2







2



d = 2R × antitan





  

2

2

lat 2 − lat1 



lon2



− lon1  



1



− sin

 \+ coos lat1 cos lat2

sin

\(

\)× \(

\)× 

  



  

2



2





   \(1\)





 



6

K. MUDULI AND I. GHOSH

Where *R* = 6.3781 × 106 m represents the radius of Earth, ***Normalization and network Layers***

and lat1, lat2, lon1, and lon2 are the latitudes and longi- The model uses layer normalization to maintain consistency in tudes of the two points, respectively. 

processing. It also includes a feed-forward network that refines 

the information further. A Global Average Pooling layer 

reduces the computational load by simplifying the output from 

***Deep learning model overview***

the Transformer encoder, making the model more efficient. 

This study introduces a novel deep-learning model using a 

Transformer architecture to predict the severity of ***Dense Layers and output***

pedestrian-vehicle interactions at unsignalized crosswalks. The network includes several dense layers with activation The Transformer is excellent at handling time-series data, functions designed to process the refined data effectively. A which is crucial for analyzing the sequence of events in Dropout layer is incorporated to prevent the model from pedestrian-vehicle interactions. The model uses a mecha- overfitting. The final output of the model is generated nism called Multi-Head Attention to focus on the most through a Dense layer with a softmax activation function, important parts of the data for predicting interaction sever- which classifies the severity of each interaction into ity. Further details of the model’s components are discussed categories. 

in the subsequent sections. 

For a detailed technical explanation of the background 

theory of the Transformer model, please refer to the 

Appendix \(supplementary file\). 

***Transformer encoder***

The Transformer encoder processes all input data, convert-

ing sequences of interactions into a format the model can ***Calculation of feature importance***

understand. This includes two main parts: multi-headed 

attention and a ful y connected network. The model Assessing the importance of each variable within the pro-ensures stability and efficiency through techniques called posed predictive model is crucial for elucidating the fac-residual connections and layer normalization. As shown in tors influencing the severity of pedestrian-vehicle 

Figure 4, the encoder processes sequences of data points, interaction. By calculating attention scores through the each representing different moments in time. The model Transformer’s attention mechanism, it becomes possible uses these data points to understand and predict the to identify which variables the model focuses on and to dynamics of pedestrian-vehicle interactions. It does this by evaluate their respective impacts on interaction severity, separating the input into three types of information: whether positive or negative. This approach offers a Queries, Keys, and Values, which help the model assess the detailed insight into how the model processes and prior-relevance of each data point to the severity of the itizes information, thereby shedding light on the critical interaction. 

factors that drive its predictions. In the Transformer 

model, the attention mechanism computes the scaled sim-

ilarity score \( *S*

***Attention mechanism***

*ij*\) by taking the dot product between the 

Query \( *Q*

The attention mechanism of the Transformer allows the 

*i*\) of a feature and the Keys \( *Kj*\) of all features 

normalized by dividing the square root of the dimension 

model to focus on the most relevant data points by creating of the Keys \(d \), as shown in Equation \(4\). 

a score for each, indicating its importance. These scores help 

k

the model prioritize which events and times are crucial for 

Q .K

predicting the severity of interactions. 



S

i

j

=



\(4\)

ij

dk

The scaled similarity scores \( *Sij*\) are normalized using a 

softmax function to generate the final attention weights \(A \), 

ij

emphasizing one feature, as shown in Equation \(5\). 

Sij



e

A =



\(5\)

ij

∑eSik

The feature importance is determined by calculating the 

average attention weight assigned to a feature across all 

instances in the dataset. The formula used to calculate the 

importance of a feature *i* is presented in Equation \(6\). 

∑ A



Importance i

ij

\( \) =



\(6\)

N

**Figure 4. ** Transform encoder architecture. 

*N* represents the number of samples used to calculate the 

note: MatMul = Matrix Multiplication; SoftMax = Softmax function; Q = query; K = key; v = value. 

attention weights of the model. 



TRAFFIC INjURY PReVeNTION

7

**Experiment setup**

incorporates a Global Average Pooling \(GAP\) layer to reduce 

dimensionality and prevent overfitting. The processed data is 

***Data preprocessing for model input***

then fed into a Multi-Layer Perceptron \(MLP\), which consists 

In this study, data preprocessing was conducted to optimize of two layers with 256 and 128 units, respectively, and includes the deep learning model’s performance. Numerical variables a 10% dropout rate to promote model generalization. The final were standardized by zero-centering their mean and scaling output is generated by a dense layer with a softmax activation their variance to one, while categorical variables like ‘Type function that classifies the interactions into severity categories: of Vehicle’ were converted to numerical values through label ‘Safe passage’, ‘Critical event’, and ‘Conflict’. The model’s archi-encoding. To ensure uniform sequence lengths, crucial for tecture is fine-tuned with a head size of 96, 4 attention heads, consistent model performance, data for each interaction was a feed-forward dimension of 192, and 2 transformer blocks, sequenced and padded as needed. 

ensuring a balance of accuracy and computational efficiency. 

The dataset, consisting of 4,315 pedestrian-vehicle interac- The details of this architecture and training process are tions from eight hours of video across two sites, was divided depicted in Figures 5 and 6. 

into training \(70%\), validation \(15%\), and testing \(15%\) sets. 

The model uses the Adam optimizer, sparse categorical 

The majority of interactions \(3,567\) were ‘Safe Passages’, with cross-entropy loss function, and accuracy as the evaluation the remainder being ‘Critical events’ \(507\) and ‘Conflicts’ metric, trained over 110 epochs with a batch size of 32. An \(214\), highlighting a class imbalance. To address this, the early stopping technique monitors the validation loss, ending Synthetic Minority Over-sampling Technique \(SMOTE\) was training if no improvement is seen over ten epochs and employed within the training set to artificial y enhance the reverting to the best model weights. This practice prevents representation of the less frequent categories. This approach is overfitting and optimizes computational resources. 

a popular technique used in the field \(Elamrani Abou Elassad 

et al. 2020; Zhang and Abdel-Aty 2022; Muduli et al. 2024;  ***Model testing***

Muduli and Ghosh 2024\) to improve the model’s ability to learn from a more balanced distribution of classes, thereby The testing phase of the model was systematical y executed enhancing the robustness and accuracy of the training process. to ensure a comprehensive evaluation of its performance on unseen data \(text data\). The trained model with optimum 

hyperparameters, equipped with its refined weights, was 

***Model training details***

employed to generate predictions for the test dataset. To 

The proposed model combines Transformer encoders and a quantitatively assess the model’s predictive efficacy, key per-Multilayer Perceptron \(MLP\) to predict pedestrian-vehicle formance metrics, as summarized in Table 5, were calculated: interaction severity at unsignalized crossings, processing 16 

input features. Each transformer encoder block includes **Results**

multi-head attention, layer normalization, and a feed-forward 

network, stacked to form the model’s core. Key hyperparame- The experimental evaluation of the model yielded promising ters such as head size, number of attention heads, feed-forward results, as delineated by a detailed confusion matrix \(Figure 7\) 

dimension, and encoder blocks are optimized using Keras and comprehensive classification metrics \(Table 6\). It is Tuner’s RandomSearch algorithm, which systematical y important to emphasize that the evaluation of the proposed explores the model space. The training process iteratively model was conducted on a test dataset derived exclusively adjusts MLP unit sizes and dropout rates to identify configu- from the original dataset, consisting of non-synthetic data, to rations that maximize validation accuracy, achieving an opti- ensure an accurate assessment of the model’s performance in mal balance of performance and efficiency. Table 4 details the real-world conditions. For Class 0 \(Safe Passage\), the model search space and optimal values for each parameter. 

showcased a precision of 0.78, a high recall of 0.91, and an 

After optimizing the hyperparameters, the model architec- F1-score of 0.84, indicating a strong propensity to correctly ture is structured as a sequence-based deep learning frame- identify safe scenarios, despite a slight tendency to misclassify work where input batches containing temporal sequences of few safe interactions as other classes. A precision of 0.78 for pedestrian-vehicle interaction features are processed through a safe passage can be acceptable for a warning system where the Transformer Encoder. This encoder uses multi-head attention 

to identify key temporal segments for severity prediction and 

**Table 4. ** optimal hyperparameters for transformer model. 

Parameter

range/Search Space

optimal value

Head Size \( *H*\)

32≤ *H* ≤ 128, Δ *H* = 32

96

number of Heads \( *Nh*\)

2≤ *Nh*≤8, Δ *Nh*=2

4

feed forward Dimension \( *F*\) 64≤ *F* ≤ 256, Δ *F* = 64

192

number of Transformer 

1≤ *B* ≤ 5, Δ *B* = 1

2

Blocks \( *B*\)

MLP units \( *U*\)

\{'64\_32', '128\_64', 

'256\_128' 

'256\_128'\}

Dropout \( *D*\)

0≤ *D* ≤ 0.5, Δ *D* = 0.1

0.1

**Figure 5. ** architecture of the proposed transformer-based model for prediction MLP Dropout \( *Dm*\)

0≤ *Dm*≤0.5, Δ *Dm*=0.1

0.1

of pedestrian-vehicle interaction severity. 





8

K. MUDULI AND I. GHOSH

**Table 5. ** Key performance metrics used for evaluating model’s predictive efficacy. 

Metric

formula

Description

Precision

True Positives

Measures the accuracy of 

the model in identifying 

True Positives \+False Positives

only true positives out of 

all positive predictions. 

recall 

True Positives

assesses the model’s ability 

\(Sensitivity\)

to capture all actual 

True Positives\+False Negatives

positive instances out of 

the actual condition 

positives. 

f1-Score

2 ×Recall× Precision

Provides a balanced measure 

of precision and recall, 

Recall \+ Precision

**Figure 7. ** confusion matrix of model predictions for three classified outcomes. 

useful in cases of uneven 

class distributions. 

accuracy

**Table 6. ** comprehensive classification metrics for three categories, with accu-True Positives\+ True Negatives

calculates the proportion of 

total correct predictions 

racy and average values. 

Total Samples

made by the model 



Precision

recall

f1-Score

across all categories. 

class 0 \(Safe 

0.78

0.91

0.84

Passage\)

class 1 \(critical 

0.93

0.85

0.89

event\)

class 2 \(conflict\)

0.95

0.86

0.9

**Accuracy**





**0.87**

**Macro avg**

0.89

0.87

0.88

**Weighted avg**

0.88

0.87

0.88

performance, with a precision of 0.95, recall of 0.86, and an 

F1-score of 0.90, suggesting exceptional precision in identify-

ing conflicts. The overall accuracy across all classes stood at 

0.87, denoting a high degree of correct predictions. The macro 

and weighted averages for precision, recal , and F1-score were 

consistently above 0.87, reflecting a uniform performance 

across classes and indicating the model’s reliable predictive 

quality, even with class imbalance considerations. These results 

affirm the model’s robustness and its applicability for classify-

ing diverse scenarios effectively. 

**Discussion**

In assessing factors influencing pedestrian-vehicle interaction 

severity, the proposed Transformer model’s attention mecha-

nism identified ‘Vehicle Speed’ as having a significant posi-

tive impact \(0.3765\). This correlation is supported by 

research from Aarts and Van Schagen \(2006\) and Gargoum and El-Basyouny \(2016\), which demonstrated that increased vehicle speeds escalate the probability of crashes. ‘Approaching 

Angle’ received a negative importance score \(0.2952\), indi-

cating that narrower angles, which reduce visibility and reac-

tion opportunities, may lead to more severe incidents, as 

discussed by Belkhouche and Bendjilali \(2013\) and supported by Harris et al. \(2023\). ‘Vehicle Distance from 

**Figure 6. ** overview of the model training procedure. 

Conflict Point’ also showed a negative score \(-0.2683\), sug-

gesting that larger distances provide more reaction time, 

cost of missing a potential y dangerous situation is much thus reducing severity, a concept reinforced by Matsui and higher than the inconvenience of a false alert. This level of Oikawa \(2019\). Additional y, ‘Type of Vehicle’ emerged as a precision can increase caution among drivers and pedestrians, positive influencer \(0.2182\), consistent with Dey et al. \(2021\), potential y reducing accidents while causing minor disrup- who found that larger vehicles tend to cause more severe tions. In the case of Class 1 \(Critical Event\), the model pedestrian road crashes. ‘Pedestrian Speed’ \(0.1583\) and achieved an impressive precision of 0.93, with a recall of 0.85 ‘Pedestrian Yaw Rate’ \(0.2898\) were also significant, indicat-and an F1-score of 0.89, demonstrating its accuracy in iden- ing that faster movements and sudden directional changes tifying critical events, though with a small margin of missed increase severity, echoing Cheng et al. \(2022\). Figure 8 visu-true events. Class 2 \(Conflict\) saw the model at its best al y il ustrates these influences, showing higher scores for 



TRAFFIC INjURY PReVeNTION

9

optical cameras captured detailed movements of pedestrians 

and vehicles, which were processed using the DataFromSky 

software to extract trajectories and convert them into 

real-world coordinates through precise georeferencing. The 

analysis focused on interactions with PET less than 10 s to 

identify potential y significant interactions. Trained observers 

then used the DataFromSky Viewer platform to classify these 

interactions into three severity categories: safe passage, critical 

event, and conflict. The reliability of these classifications was 

confirmed using the Fleiss Kappa statistic, indicating substan-

tial inter-rater agreement with a coefficient \(𝜅=0.75\). 

The model was trained on dynamic input variables repre-

senting detailed pedestrian and vehicle dynamics derived from 

the trajectory data and balanced using SMOTE. It was then 

evaluated on a separate test dataset, demonstrating high effec-

tiveness across different severity categories. For safe interactions 

\(Class 0\), the model achieved a precision of 0.78, a recall of 

**Figure 8. ** attention-based variable importance ranking. 

0.91, and an F1-score of 0.84. Critical events \(Class 1\) and con-

flicts \(Class 2\) showed even higher precision and recal , il us-

trating the model’s ability to accurately identify and classify the 

factors like vehicle speed and pedestrian yaw rate, which most hazardous situations. Overall accuracy was recorded at significantly impact severity while highlighting the preventa- 0.87, with consistent macro and weighted averages for preci-tive potential of greater distances from conflict points. 

sion, recal , and F1-score above 0.87. The variable importance 

The fact that these findings are general y in line with pre- analysis using the model’s attention mechanism highlighted key vious studies suggests that the proposed transformer-based factors affecting interaction severity. ‘Vehicle Speed’ emerged as deep learning approach for predicting interaction severity is a significant factor, with higher speeds increasing severity due working correctly, and the model learns to predict the inter- to greater impact forces and longer stopping distances. In con-action severity in an accurate manner. This alignment rein- trast, ‘Approaching Angle’ and ‘Vehicle Distance from Conflict forces the reliability and validity of the proposed methodology Point’ had negative importance scores, suggesting that nar-and supports its potential for practical applications in rower angles and greater distances might reduce severity by enhancing pedestrian safety. 

improving visibility and reaction times. Additional y, ‘Type of 

Vehicle’, along with pedestrian behaviors such as ‘Pedestrian 

**Conclusions**

Speed’ and ‘Pedestrian Yaw Rate’, were significant, linking the 

type of vehicle to the impact severity and pedestrian behaviors 

This study introduces a novel approach to assessing to increased risk due to sudden movements. These findings pedestrian-vehicle interaction severity at crosswalks, leverag- il ustrate the complex interaction of behavioral and environ-ing a novel deep learning model that uniquely combines mental factors in pedestrian-vehicle dynamics. 

Transformer-based architectures with Multilayer Perceptrons 

This study has certain limitations, including the omission 

\(MLP\). This model integrates the sophisticated time-series of environmental factors like weather conditions and archi-data handling capabilities of Transformer architectures tectural features, which could have strengthened the assess-renowned for their effectiveness in capturing sequential ments. Additional y, intrinsic factors such as psychological dependencies through attention mechanisms, which allow traits and individual differences among traffic participants the model to focus on the most relevant features of the data merit further exploration in subsequent studies. Future over time. In conjunction with the classification prowess of research should consider integrating contextual variables like MLPs, which analyze the transformed features to predict time of day and road surface conditions to enhance the pre-interaction severity, the model provides a robust and inter- cision of severity predictions. Adapting the model for pretable framework. This dual approach enables a more real-time analysis could enable immediate feedback and nuanced understanding of complex pedestrian and vehicle warnings at high-risk crosswalks, enhancing pedestrian and dynamics at unsignalized intersections, significantly enhanc- driver safety. Moreover, expanding the methodology to ing prediction accuracy and interpretability compared to account for interactions involving vehicular traffic and existing methods, such as those used by Zhang and cyclists would broaden the scope of safety assessments in Abdel-Aty \(2022\), who achieved the highest accuracy of urban environments. By deploying this model across varied 0.723 in predicting pedestrian-vehicle interaction severity settings, its effectiveness can be validated across different using an Extreme Gradient Boosting \(XGBoost\) model after cultural and traffic contexts, contributing significantly to employing various techniques like random forests, support global pedestrian safety initiatives. 

vector machines, logistic regression, gradient boosting 

machines, and linear discriminant analysis. 

Data was initial y collected from eight hours of video sur- **Disclosure statement** veil ance at two unsignalized intersections. High-resolution No potential conflict of interest was reported by the author\(s\). 

10

K. MUDULI AND I. GHOSH

**Funding**

ments: a systematic review. IEEE Trans Intell Transport Syst. 

24\(11\):11544–11567. doi:10.1109/TITS.2023.3291196. 

This work was supported by the Science and Engineering Research Han IC, Luan BC, Hsieh FC. 2014. Development of autonomous emer-Board \(SERB\), Government of India, under the Core Research Grant 

gency braking control system based on road friction. IEEE 

Scheme, awarded for the project “Machine Learning Framework for the 

International Conference on Automation Science and Engineering. 

Development of an Interactive Pedestrian Crossing to Enhance 

2014-January: p. 933–937. doi:10.1109/COASE.2014.6899438. 

Pedestrian Safety,” Sanction Order No. CRG/2023/003239. 

Harris L, Ahmad N, Khattak A, Chakraborty S. 2023. Exploring the effect of visibility factors on vehicle–pedestrian crash injury severity. Transp Res Rec \[Internet\]. 2677\(11\):24–35. doi:10.1177/03611981231164070/

**ORCID**

ASSET/IMAGES/LARGE/10.1177\_03611981231164070-FIG3.JPEG. 

Hayward JC. 1972. Near-miss determination through use of a scale of Kaliprasana Muduli http://orcid.org/0000-0003-3504-2086

danger. Highway Research Record. 384:24–34. 

Indrajit Ghosh http://orcid.org/0000-0002-1341-0258

Hydén C, Linderholm L. 1984. The Swedish traffic-conflicts technique. 

International Calibration Study of Traffic Conflict Techniques. 

5:133–139. doi:10.1007/978-3-642-82109-7\_12. 

**Data availability statement**

Kathuria A, Vedagiri P. 2020. Evaluating pedestrian vehicle interaction The datasets from this study are available from the authors upon 

dynamics at un-signalized intersections: a proactive approach for safe-ty analysis. Accid Anal Prev. 134:105316. doi:10.1016/j.aap.2019.105316. 

reasonable request. 

Landis JR, Koch GG. 1977. The measurement of observer agreement for categorical data. Biometrics. 33\(1\):159–174. doi:10.2307/2529310. 

**References**

Li P, Guo H, Bao S, Kusari A. 2022. A Probabilistic Framework for Estimating the Risk of Pedestrian-Vehicle Conflicts at Intersections 

Aarts L, Van Schagen I. 2006. Driving speed and the risk of road crashes: 

\[Internet\]. \[accessed 2023 Apr 15\]. https://arxiv.org/abs/2207.14145v1. 

a review. Accid Anal Prev. 38\(2\):215–224. doi:10.1016/j.aap.2005.07.004. 

Matsui Y, Oikawa S. 2019. Situational characteristics of fatal pedestrian Adamec V, Herman D, Schullerova B, Urbanek M. 2020. Modelling of accidents involving vehicles traveling at low speeds in Japan. Traffic traffic load by the datafromsky system in the smart city concept. In: Inj Prev. 20\(sup1\):S1–S6. doi:10.1080/15389588.2019.1587166. 

Lopes N, editor. Smart governance for cities: Perspectives and expe-

Mohammadian S, Haque MM, Zheng Z, Bhaskar A. 2021. Integrating riences. EAI/Springer innovations in communication and computing. 

safety into the fundamental relations of freeway traffic flows: a 

Cham: Springer. p. 135–152. doi:10.1007/978-3-030-22070-9\_7. 

conflict-based safety assessment framework. Anal Methods Accid 

Allen BL, Shin BT, Cooper PJ. 1978. Analysis of traffic conflicts and Res. 32:100187. doi:10.1016/j.amar.2021.100187. 

collisions. Transp Res Rec. 667:67–74. 

MORTH. 2022. Road accidents in india 2020. Ministry of Road Transport Ankit Bansal, Tripta Goyal, Umesh Sharma. 2018. Pedestrian safety on and Highways \[Internet\]. \[accessed 2022 Jul 22\]. www.morth.nic.in. 

crosswalks in India – Need of the hour. J. Today’s Ideas - Tomorrow’s Muduli K, Ghosh I. 2024. Prediction of Vehicular Yielding Intention Technol. 6\(1\):35–46. doi:10.15415/jotitt.2018.61004. 

While Approaching a Pedestrian Crosswalk. \[Internet\]. \[accessed 

Belkhouche F, Bendjilali B. 2013. Dynamic collision risk modeling un-2024 Jun 23\]. doi:10.1177/03611981241252835. 

der uncertainty. Robotica \[Internet\]. 31\(4\):525–537. doi:10.1017/

Muduli K, Sahu V, Ghosh I. 2024. Predicting pedestrian movement in 

S0263574712000550. 

unsignalized crossings: a contextual cue-based approach. 2024 16th 

Cheng R, Pan Y, Xie L. 2022. Analysis of vehicle-pedestrian accident International Conference on COMmunication Systems & NETworkS 

risk based on simulation experiments. Math Probl Eng. 2022:1–14. 

\(COMSNETS\) \[Internet\]. \[accessed 2024 Mar 5\]: 204–209. 

doi:10.1155/2022/7891232. 

doi:10.1109/COMSNETS59351.2024.10427345. 

Cooper PJ. 1984. Experience with traffic conflicts in canada with em-Mukherjee D, Mitra S. 2019. A comparative study of safe and unsafe phasis on “post encroachment time” techniques. International 

signalized intersections from the view point of pedestrian behavior 

Calibration Study of Traffic Conflict Techniques \[Internet\]. 5:75–96. 

and perception. Accid Anal Prev \[Internet\]. 132\(April\):105218. 

doi:10.1007/978-3-642-82109-7\_8. 

doi:10.1016/j.aap.2019.06.010. 

Deep traffic video analysis – DataFromSky. \[accessed 2024 Mar 12\]. Ni Y, Wang M, Sun J, Li K. 2016. Evaluation of pedestrian safety at inter-

https://datafromsky.com/. 

sections: a theoretical framework based on pedestrian-vehicle interac-Dey D, Matviienko A, Berger M, Martens M, Pfleging B, Terken J. 

tion patterns. Accid Anal Prev. 96:118–129. doi:10.1016/j.aap.2016.07.030. 

2021. Communicating the intention of an automated vehicle to pe-Nie B, Li Q, Gan S, Xing B, Huang Y, Li SE. 2021. Safety envelope of destrians: the contributions of eHMI and vehicle behavior. IT – 

pedestrians upon motor vehicle conflicts identified via active avoid-

Information Technology \[Internet\]. 63\(2\):123–141. doi:10.1515/

ance behaviour. Sci Rep. 11\(1\):1–10. doi:10.1038/s41598-021-82331-z. 

ITIT-2020-0025/MACHINEREADABLECITATION/RIS. 

Paul M, Ghosh I. 2020. Post encroachment time threshold identifica-Dhatbale R, Bhargava ·, Chilukuri R. 2021. Deep Learning Techniques tion for right-turn related crashes at unsignalized intersections on 

for Vehicle Trajectory Extraction in Mixed Traffic. J. Big Data Anal. 

intercity highways under mixed traffic. Int J Inj Contr Saf Promot. 

Transp. 3\(2\):141–157. doi:10.1007/s42421-021-00042-3. 

27\(2\):121–135. doi:10.1080/17457300.2019.1669666. 

Elamrani Abou Elassad Z, Mousannif H, Al Moatassime H. 2020. Rasouli A, Tsotsos JK. 2020. Autonomous vehicles that interact with Class-imbalanced crash prediction based on real-time traffic and 

pedestrians: A survey of theory and practice. IEEE Trans Intell 

weather data: a driving simulator study. Traffic Inj Prev. 21\(3\):201–

Transport Syst. 21\(3\):900–918. doi:10.1109/TITS.2019.2901817. 

208. doi:10.1080/15389588.2020.1723794. 

Selmoune A, Yun J, Seo M, Kwon H, Lee C, Lee J. 2023. Development Ezzati Amini R, Yang K, Antoniou C. 2022. Development of a conflict risk of a residential road collision warning service based on risk assess-evaluation model to assess pedestrian safety in interaction with vehicles. 

ment. J Adv Transp. 2023:1–16. doi:10.1155/2023/7496377. 

Accid Anal Prev. 175:106773. doi:10.1016/J.AAP.2022.106773. 

Shahdah U, Saccomanno F, Persaud B. 2014. Integrated traffic conflict Fleiss JL. 1971. Measuring nominal scale agreement among many rat-model for estimating crash modification factors. Accid Anal Prev. 

ers. Psychol Bul . 76\(5\):378–382. doi:10.1037/h0031619. 

71:228–235. doi:10.1016/j.aap.2014.05.019. 

Formosa N, Quddus M, Ison S, Abdel-Aty M, Yuan J. 2020. Predicting Van der Horst R, Kraay RJ. 1986. The Dutch Conflict Technique—

real-time traffic conflicts using deep learning. Accid Anal Prev. 

DOCTOR. *ICTCT Workshop* Budapest. 

136:105429. doi:10.1016/j.aap.2019.105429. 

WHO. 2018. Global status report on road safety 2018. World Health 

Gargoum SA, El-Basyouny K. 2016. Exploring the association between Organization \[Internet\]. \[accessed 2022 Jul 22\]. http://apps.who.int/

speed and safety: a path analysis approach. Accid Anal Prev. 93:32–

bookorders. 

40. doi:10.1016/j.aap.2016.04.029. 

Zhang S, Abdel-Aty M. 2022. Real-Time Pedestrian Conflict Prediction Golchoubian M, Ghafurian M, Dautenhahn K, Azad NL. 2023. 

Model at the Signal Cycle Level Using Machine Learning Models. IEEE 

Pedestrian trajectory prediction in pedestrian-vehicle mixed environ-

Open J Intell Transp Syst. 3:176–186. doi:10.1109/OJITS.2022.3155126. 



# Document Outline

+ Predicting pedestrian-vehicle interaction severity at unsignalized intersections  
	+ ABSTRACT 
	+ Introduction 
	+ Methods  
		+ Data sources 
		+ Dataset preparation  
			+ Behavior observation and interaction severity estimation 


	+ Classification schemes  
		+ Safe passage 
		+ Critical event 
		+ Conflict  
			+ Assessment of observer agreement in severity level estimation 
			+ Input variables 

		+ Deep learning model overview  
			+ Transformer encoder 
			+ Attention mechanism 
			+ Normalization and network Layers 
			+ Dense Layers and output 

		+ Calculation of feature importance 

	+ Experiment setup  
		+ Data preprocessing for model input 
		+ Model training details 
		+ Model testing 

	+ Results 
	+ Discussion 
	+ Conclusions 
	+ Disclosure statement 
	+ Funding 
	+ ORCID 
	+ Data availability statement 
	+ References



