COMSNETS 2024: Intelligent Transportation Systems Workshop Predicting Pedestrian Movement in Unsignalized Crossings: A Contextual Cue-Based Approach Kaliprasana Muduli 

Vikas Sahu 

Indrajit Ghosh 

*PhD Scholar, Civil Engineering *

*M. Tech Student, Mehta Family School* *Associate Professor, Civil Engineering* *Department * 

*of Data Science and Artificial *

*Department & Joint Faculty, Mehta* *Indian Institute of Technology Roorkee* *Intelligence* 

*Family School of Data Science and *

Roorkee, India 

*Indian Institute of Technology Roorkee* *Artificial Intelligence* 

k\_muduli@ce.iitr.ac.in 

Roorkee, India 

*Indian Institute of Technology Roorkee* vikas\_s@mfs.iitr.ac.in 

Roorkee, India 



indrafce@iitr.ac.in 



***Abstract— To ensure safe and secure coexistence between ***

the speed of pedestrian crossings, that medians lessen the 

***pedestrians and autonomous vehicles \(AVs\), AVs must be able to ***

frequency of changes in crossing behavior, that the size of the 

***anticipate pedestrian behavior and respond to it. This research ***

grouping of pedestrians reduces the variation in their crossing 

***gathers video data from real traffic scenes to predict pedestrian ***

pace, and that there is a significant speed shift as faster-

***crossing intentions at unsignalized crossings. Computer vision ***

moving cars approach. In a survey conducted in Bengaluru, 

***techniques such as YOLOv4, Deep SORT, and perspective ***

India, Nicholas N. Ferenchak \[5\] discovered a high 

***transformation are employed for road user detection, tracking, ***

***and mapping image coordinates to world coordinates to prepare ***

correlation between age and gender in terms of pedestrian 

***trajectory datasets. Using trajectory data, several features ***

behavior at midblock crossings. Older persons were more 

***influencing pedestrian intention like walking speed, location in the ***

careful, but male pedestrians were riskier than females. 

***road environment, count and direction of approaching traffic, ***

Waiting times, using crosswalks, and interactions with 

***speed and type of closest approaching vehicle upstream, etc., are ***

moving vehicles were all influenced by age and gender. 

***extracted. The dataset for this study was obtained by analyzing ***

Additionally, discovered that larger groups exhibit riskier 

***1,411 pedestrians, resulting in 223,136 samples. To predict ***

behavior in comparison to smaller groups \[6\]. The types of 

***pedestrian crossing intentions, LSTM and Bi-LSTM with an ***

vehicle and volume of traffic also affect pedestrian behavior 

***attention mechanism model were built and trained to anticipate ***

as observed in the survey conducted by Asaithambi et al. \[7\] 

***the pedestrian crossing intention at unsignalized crossing. The ***

***proposed model successfully combined the characteristics and ***

in Mangalore, India. There are a number of other features, 

***surrounding dynamics of pedestrians to produce accurate ***

including a pedestrian’s pose, that help predict pedestrian 

***predictions, Bi-LSTM with an attention mechanism outperformed ***

intention. However, in countries like India, where non-lane-

***LSTM, achieving an AUC of 95.3%, 91.1%, 89.2%, 87.5%, and ***

based heterogeneous traffic condition prevails, pedestrians’ 

***84% on the testing dataset at unsignalized crossing on the 0.6 sec, ***

intention to cross the road largely depends on surrounding 

***1.2 s, 1.8 s, 2.4 s, and 3 s time horizons. These outcomes can be ***

dynamics. This study uses contextual cues like closest vehicle 

***used to improve Connected and Autonomous Vehicle \(CAV\) ***

speed, distance, vehicle count, etc., as input variables to 

***technologies, infrastructure-to-vehicle \(I2V\) connectivity, and ***

predict pedestrians’ intentions. 

***driver assistance systems to enhance pedestrian safety while ***



Recurrent neural networks \(RNNs\), in particular, 

***navigating through pedestrian crosswalks. ***

have been studied as a potential deep learning model for 

***Keywords— Pedestrian Crossing Intention Prediction, ***

predicting pedestrian intention by several academics. RNNs 

***Unsignalized Crossings, Computer vision, Attention. ***

work by transferring outputs from the one-time frame in one I. INTRODUCTION 

layer to the next. RNNs, however, have problem when there is a large enough delay between the input and the unit \[8\]\[9\]. 

Pedestrian safety is a crucial issue in modern transportation A particular kind of RNN called LSTM was created to systems, and it has drawn the attention of policymakers, represent 

sequential 

data 

by 

capturing 

long-term 

planners, and researchers worldwide. In recent years, the dependencies \[10\]. Long short-term memory \(LSTM\) was number of accidents involving pedestrians has increased, used by Ghori et al. \[11\] to complete the sequence modeling particularly at unsignalized crossings where pedestrian-challenge of pedestrian intention prediction. A modified form vehicle interactions are largely unregulated. According to of LSTM called social LSTM was developed by Alahi et al. 

India’s Ministry of Road Transport and Highway \(MoRTH\) 

\[12\] to forecast walkers’ trajectories based on their social report, 29,124 pedestrians died in 2021 which account for interactions in congested environments. As seen by their 18.9% of total road accident fatalities \[1\]. According to successful applications in pedestrian intention and path 2019 data, approximately 46% of the fatalities in Delhi, the prediction over the past few years, LSTM models have capital of India, and 35% of those killed in traffic accidents proven to be the most successful models for anticipating in Chandigarh, India were pedestrians \[2\]\[3\]. 

walkers’ unexpected crossings, whether using posture Predicting pedestrian intention is complex, and many sequences or historical trajectory data. Zhang Set al. \[13\] 

dynamic road scenarios affect pedestrian behavior. As the used LSTM for predicting pedestrian intention considering world moves toward autonomous vehicles \(AV\), researchers some contextual features, however as discussed earlier, many have conducted in-depth surveys to identify the variables contextual features that influence pedestrian behaviors in influencing pedestrian behavior. Kadali and Vedagiri \[4\] 

developing countries like India have not been considered. 

conducted a survey in Mumbai, India to examine pedestrian Jaywalking is an act when pedestrians cross the road speed behavior in traffic and found that insufficient space without following the traffic rules involves sudden and between pedestrians and vehicles has a significant impact on unpredictable movements. The presence and actions of nearby motor vehicle traffic greatly impact it. This behavior 2024 16th International Conference on COMmunication Systems & NETworkS \(COMSNETS\) | 979-8-3503-8311-9/24/$31.00 ©2024 IEEE | DOI: 10.1109/COMSNETS59351.2024.10427345



Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 12:13:22 UTC from IEEE Xplore. Restrictions apply. 

979-8-3503-8311-9/24/$31.00 ©2024 IEEE

204



COMSNETS 2024: Intelligent Transportation Systems Workshop is especially common in developing countries like India, **Object detection: **In this work, YOLOv4\[17\] algorithm was where it poses a serious risk to pedestrian safety when they used for road user detection. YOLOv4 is a cutting-edge object engage with moving automobiles, particularly at unsignalized detection algorithm that achieves high accuracy and speed in crossing locations. This risk is only likely to grow as detecting multiple objects in real time. YOLO is faster than connected and autonomous vehicles become more common. 

two-stage object detection algorithms because it uses a single-In low-trust situations \(such as aggressive AV driving at stage detector that directly predicts object bounding boxes and unsignalized crosswalks\), Jayaraman S et al. \[14\] discovered class probabilities in a single forward pass through the that using an explicit communication interface is one way to network without the need for an extra region proposal network \(RPN\) stage. In contrast, two-stage detectors, such as Faster express the pedestrian intention to an AV. This can reduce R-CNN, require a separate RPN stage to generate region uncertainty and increase AV trust. Nevertheless, despite this proposals, which are then fed into the object detection network urgent issue, there has not been much focus on developing for final detection \[18\]\[19\]. ** **

reliable techniques for forecasting the behavior of pedestrians. Numerous studies in the literature have aimed to **Object tracking: **The process of tracking the movements of forecast pedestrian crossing intentions by analyzing historical objects is called Multiple Object Tracking \(MOT\), and it has trajectory and pose sequences. However, in the Indian been widely used in various applications. In this study, the context, where non-lane-based heterogeneous traffic is Deep SORT algorithm \[20\]\[21\] was employed for object prevalent, pedestrian intentions are significantly influenced tracking, which has demonstrated high performance on the by the surrounding context, which has largely been MOT16 Challenge benchmark \[22\]. The Deep SORT 

algorithm utilizes a combination of deep neural networks for overlooked in many earlier studies. This study investigates both object detection and tracking. Initially, the YOLOv4 

the application of computer vision and deep learning algorithm is used to detect and classify road users, and then methodologies to predict the future state of pedestrians while the Deep SORT algorithm takes the detection boxes as input crossing the road, incorporating various critical parameters to track the movement of each road user. 

related to local dynamics. 

**Perspective Transformation: **In this work, the perspective II. DATA COLLECTION 

transformation technique has been used to convert the location *A. Study Site *

of an object in an image from image coordinates to world coordinates. This conversion is accomplished using a To select a suitable location for the study, certain homography matrix \(ℎ\), which relates the image plane to the prerequisites needed to be fulfilled, including a high volume world plane. As shown in \(Equation 1\), the homography of pedestrians, unsignalized crossing, and records of the matrix contains nine values, which are used to transform the accident. A stretch of an uncontrolled crossroads at Cheema image coordinates \( u , v \) to their corresponding world Chowk, Panjab, India, was chosen for the study after coordinates \(X, Y\). The homography matrix is calculated by consultation with local police stations. The location was finding the transformation that maps a set of points in the chosen due to the high volume of pedestrians and the non-image plane to their corresponding points in the world plane. 

availability of proper signalized crossing. A study by Muduli These points are typically defined by a set of image et al. \(2023\) indicated that the study site was a hotspot for coordinates \( , \) and their corresponding world coordinates pedestrian crashes. Using an optical camera mounted on a \(

, \), \(which are obtained using a GPS\). The process of nearby fly-over, video data were captured for 4 hours in the calculating the homography matrix involves using a linear morning and evening hours of typical weekdays. The area least squares method \[23\]\[24\] and singular value under consideration consists of a dual carriageway with two decomposition. Once the homography matrix has been lanes in each direction, separated by a physical median. The calculated, it can be used to transform all image coordinates site’s spatial map, which shows the study area and camera to their corresponding world coordinates \(Equation 1\). 

mounting location, is presented in Figure 1. 

u

h h

h X

X



v h h h Y h Y 

1

h h

h 1

1

X

u

=> Y h

v 

1

1

1 

\( , \): Coordinate of each point on the image plane \(

, \): Coordinate of each point on the world plane Figure 1. Satellite Image of the site of study. 

The haversine formula is used for calculating the speed of moving road users between time and \(Equation 2\). 

*B. Video Processing *

\!""\#

To process the gathered video data from the study site, ℎ$ "%&'\(" 

, , 

, 

deep learning-based computer vision techniques are utilized. 



\* 



2 

The main objectives of this processing are to extract road users’ trajectories. The computer vision techniques used for The flowchart of the data extraction process is shown in Figure 2. 

this purpose include object detection, object tracking, and perspective transformation, similar to the approaches used by Muduli & Ghosh \(2023\). 

205

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 12:13:22 UTC from IEEE Xplore. Restrictions apply. 





COMSNETS 2024: Intelligent Transportation Systems Workshop Nearer to Starting curb \(0\), 

Pedestrian 

nearer to the first centerline 

location in the 

\(1\), nearer to the median 

Nominal 

road 

\(2\), nearer to the second 

categorical 

environment 

centerline \(3\), nearer to the 

ending curb \(4\) 

Speed of closest 

Speed of the nearest 

approaching 

Continuous 

approaching vehicle in m/s. 

vehicle 

Closest Vehicle 

Distance in \(m\) 

Continuous 

Distance 

No vehicle \(0\), Bicycle \(1\), 

Type of closest 

Motorbike \(2\), Car, van, 

Nominal 

approaching 

tuk-tuk \(3\), Light Truck 

categorical 

vehicle 

\(4\), Truck \(5\), Bus \(6\) 

Approaching 

Total number of 

Numeric 

vehicle count 

approaching vehicles 

Male \(0\), 

Nominal 



Gender 

Female \(1\) 

categorical 

Figure 2. Flowchart of data extraction process Whether the pedestrian is 

walking in a group, no 

Nominal 

III. METHODOLOGY 

Grouping 

grouping \(0\), group of two 

categorical 

\(1\), group of three \(2\), 

*A. Input Variable *

group of four or more \(3\), 

Child \(0\), Teen \(1\), Mid-

Nominal 

Pedestrian crossing intention can be influenced by various Age group 

age \(2\), Old-age \(3\) 

categorical 

parameters, such as the speed of pedestrians, the direction of **t n**

oncoming traffic, the location of pedestrians relative to the **ed**

Whether the pedestrian 

Crossing 

Nominal 

road environment, gender, grouping, closest approaching **ne**

will cross. Crossing \(1\), 

**p**

intention 

categorical 

**e**

Waiting \(0\) 

vehicle description, etc. Five categories are used to categorize **D**

the pedestrian’s position in relation to the road environment: closer to the beginning curb, closer to the first centerline, *C. Model Development *

closer to the median, closer to the second centerline, and In this research recurrent neural networks \(RNNs\) based closer to the finishing curb. This classification is used to models, Long Short-Term Memory \(LSTM\), and Bi-maintain flexibility across roads with varying numbers of directional Long Short-Term Memory \(Bi-LSTM\) with lanes rather than relying on lane numbers as a variable. 

attention model used to predict pedestrian crossing intentions based on the characteristics of the pedestrians and B. Pedestrian crossing intention labeling * *

surrounding dynamics at the unsignalized pedestrian A time-series dataset was created from the trajectories of crossing. Since pedestrian trajectories involve time-series pedestrians, and the dependent variable Y was labeled to data, these RNN-based models can effectively capture the indicate whether the pedestrian intended to cross the crossing. 

temporal dependencies of pedestrian trajectories, crucial for The behavior of pedestrians were observed in two stages, intention prediction. 

namely waiting and crossing, and the dependent variable Y 

**LSTM: **Long Short-Term Memory \(LSTM\) unit provides a was labeled based on their behavior, as shown in Figure 3. 

method to selectively allow information to pass through by deleting or adding some information through the gate structure. This is the key to this network. To retain and update the cell state, the LSTM unit has three gate structures \(input gate, forget gate, and output gate\). The three gate structures and the memory cell state corresponding to time * * t are represented here by the symbols '- , .- , /- , and 0- 

\(a\) Crossing 

\(b\) Waiting 

respectively. 



Figure 3. Pedestrian intention labeling 

Forget gate \(.-\) eliminates some data from the memory For prediction, a prediction horizon of 0.6s, 1.2s, 1.8s, 2.4s, cells, input gate \( '- \) determines which new information and 3s were used. Hence, annotated labels were advanced by should be kept in the cell state, output gate \(/-\) collects the respective time to prepare the data set. Table I summarizes all output information in the end. information flow in LSTM is of the independent and dependent variables along with their regulated by these three gates. 

descriptions. 

.- 12345ℎ- , 6-7 8 94: 3 ** **



TABLE I. 

INDEPENDENT AND DEPENDENT VARIABLES 

'- 1 3 5ℎ- , 6-7 8 9 4 



**Variables **

**Variable Description **

**Type **

0- .- ∙ 0- 8 '- ∙ tanh 3@5ℎ- , 6-7 8 9@ 5 

**t **

Speed 

of 

**n**

Speed of pedestrian m/s 

Continuous 



**e**

pedestrian 

**d**

**le **

/

**n**

**b**

-

1 3B5ℎ- , 6-7 8 9B 6 

**e**

Vehicle approaching 

**ia**

**p**

**r **The direction of 

**e**



**a**

direction with respect to 

Nominal 

**d**

**v **Approaching 

pedestrian, for right side 

categorical 

ℎ

**In**

Vehicle 

-

/- ∙ tanh 0- 7 

\(0\), for left side \(1\) 



206

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 12:13:22 UTC from IEEE Xplore. Restrictions apply. 





COMSNETS 2024: Intelligent Transportation Systems Workshop E- 3F ∙ ℎ- 8 9F 8 

hidden states is also known as the context vector 0 \(equation 11\). 

1 = Sigmoid Activation function. 



3 = Weight matrices 

"-

. ℎ- 9 

b = Bias 



6

exp " 

- = input vector 

$

-

10

ℎ

-

O



- = Hidden output vector 

∑ P  

E

QR exp 2"Q:

- = output vector 



OP

c U   $-ℎ- 11 

-R



were, 

"- : Alignment score at time . 

$- : Weight at time . 

0 : Context vector. 





Figure 4: Architecture of LSTM model 

Output vector \(E-\) is computed using equation \(3\) to equation \(8\). Figure 4 shows the LSTM model architecture that was applied in this work. The model consists of an input layer, a stacked LSTM layer, a dense \(fully linked\) layer, and an output neuron that represents the classification result. 

Additionally, the dropout layer is included to avoid overfitting. For optimization, the Adam function is used. The final output is obtained using the Sigmoid activation function. 

**Bi-LSTM with attention: **Bi-LSTM \(Bi-directional LSTM\) neural network model can effectively capture the temporal dependencies of pedestrian trajectories by processing the Figure 5: Architecture of Bi-LSTM with the attention input sequence in both forward and backward directions. An mechanism 

attention mechanism is added to the Bi-LSTM to improve its capacity to concentrate on important parts of the input sequence. The model can give varying weights to the input The architecture of Bi-LSTM with the attention mechanism sequence. As a result, the model can focus on the portions of used in this study, is shown in Figure 5. The architecture the input that are most important for making predictions. In consists of multiple layers. First, the input layer order to determine the relative significance of each time accommodates the time-series data. Second, two layers of Bi-step’s hidden state for the outcome prediction, attention LSTM are applied to the input sequence to process the weights are computed for each time step. The learning sequence. Third, the attention layer is utilized to concentrate function . \(equation 9\), which is implemented using a feed-on the relevant part of the sequence, then the attention output forward network, is used to compute the alignment score. The is flattened to prepare for further processing. Finally, a dense alignment scores are normalized using the softmax function layer with a sigmoid activation function is used to produce \(equation 10\) to get a distribution of weights that adds up to binary classification output, indicating pedestrian future 1. The model can concentrate on the most relevant portions crossing intention. 

of the time series by taking a weighted sum of the hidden states using the attention weights. The weighted sum of the 207

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 12:13:22 UTC from IEEE Xplore. Restrictions apply. 

COMSNETS 2024: Intelligent Transportation Systems Workshop IV. EXPERIMENTS AND RESULTS 

and Bi-directional Long Short-Term Memory \(Bi-LSTM\) with attention model was evaluated in the time horizon of The Bi-LSTM with attention mechanism model was built to 0.6s, 1.2s, 1.8s, 2.4s, and 3s . The evaluation matrices’ results predict pedestrian intention at unsignalized crossings are shown in Table II. The performance metrics \(AUC, environment, The hyperparameters of the model are tuned Precision, Accuracy, and F1-Score\) often fall with an such that it will achieve the best performance. 

increase in prediction horizon, as can be seen for both models. 

*A. Evaluating metrics *

This implies that the accuracy of the model’s predictions declines with increasing prediction horizons. Predicting The following evaluation matrices were used to check the pedestrian crossing intentions accurately at shorter time performance of the proposed model: 

horizons is somewhat expected due to the immediacy of the decision-making process involved. The predictions are more Accuracy: The proportion of correctly classified instances out accurate because the model, at a shorter time frame, covers of the total number of instances, as shown in Equation \(6\). 

the most immediate, deliberative behaviors of pedestrians V00 %$0E 

when deciding to cross. Although both models perform satisfactorily, bi-LSTM with attention outperforms LSTM in OWXY ZB\[ - \\Y\]OWXY ^Y\_\`- \\Y

\(6\) 

OWXY ZB\[ -\\Y\]àb\[Y ZB\[ - \\Y\]àb\[Y ^Y\_\`- \\Y\]OWXY ^Y\_\`- \\Y

all metrics at all time horizons proving its robustness for handling longer time sequences. The Bi-LSTM's attention Precision: The proportion of accurately identified samples mechanism enables the model to concentrate on more among positively classified samples, as shown in Equation important temporal data, improving effectiveness in \(7\). 

capturing pedestrians’ behavior. 





c%"0'&'/\( 

OWXY ZB\[ - \\Y

7 

TABLE II. EVALUATION MATRICES’ RESULTS 

OWXY ZB\[ -\\Y\]àb\[Y ZB\[ - \\Y





Recall \(also known as sensitivity or true positive rate\): The n



n

re 



proportion of correctly identified samples among genuine rizoo

el d

racy

co

C

o

U

positive samples, as shown in Equation \(8\). 

ecall 

e H

-S

M

ccu

R

recisio

1

A

A

P

F



imT

d"0$ee 

OWXY ZB\[ - \\Y

8 

OWXY ZB\[ -\\Y\]àb\[Y ^Y\_\`- \\Y





LSTM 

0.873 

0.938 

0.834 

0.883 

0.934 

0.6 

F1-score: The harmonic mean of precision and Recall, as sec 

Bi-LSTM 

shown in Equation \(9\). 

with 

0.919 

0.948 

0.897 

0.922 

0.953 



Attention 

f1&0/%" ∗ZWY@ \[ Bh∗iY@\`bb 9

ZWY@ \[ Bh\]iY@\`bb

LSTM 

0.833 

0.823 

0.845 

0.834 

0.875 





1.2 

AUC \(Area Under the ROC Curve\): The performance sec 

Bi-LSTM 

metric used to evaluate the effectiveness of a binary with 

0.854 

0.836 

0.868 

0.851 

0.911 

Attention 

classification model. It represents the total area under the receiver operating characteristic \(ROC\) curve, which plots the LSTM 

0.814 

0.880 

0.775 

0.828 

0.864 

true positive rate against the false positive rate at various 1.8 

threshold settings. 

sec 

Bi-LSTM 

*B. Experiment Results *

with 

0.854 

0.909 

0.820 

0.862 

0.892 

Attention 

In this discussion, 4 hours of video data were collected from the study site, which has data of 1,411 pedestrians. The LSTM 

0.819 

0.897 

0.777 

0.833 

0.839 

pedestrian data are split into training sets \(80%\) and test sets 2.4 

\(20%\) sets in order to train and test the performance of both sec 

Bi-LSTM 

proposed models. There was a total of 223,236 instances, out with 

0.844 

0.917 

0.799 

0.854 

0.875 

of which 202,753 were positive and 20,383 were negative Attention 

instances. 



An imbalanced distribution of data will cause poor LSTM 

0.814 

0.866 

0.785 

0.823 

0.811 

performance of the model. The synthetic minority over-3 

sec 

sampling method \(SMOTE\)\[25\] is utilized to artificially Bi-LSTM 

produce additional data on the minority class in order to with 

0.854 

0.887 

0.830 

0.858 

0.840 

Attention 

address the data imbalance in this work. SMOTE is a well-known machine learning approach to handling unbalanced data. To balance the class distribution, it operates by V. CONCLUSION 

generating artificial cases of the minority class in a dataset. 

SMOTE operates by locating minority class instances and This study presents a deep-learning approach using LSTM 

interpolating between them to produce new synthetic and Bi-LSTM with an attention mechanism for predicting instances. The proposed Long Short-Term Memory \(LSTM\) pedestrian crossing intentions at an unsignalized crossing in 208

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 12:13:22 UTC from IEEE Xplore. Restrictions apply. 

COMSNETS 2024: Intelligent Transportation Systems Workshop Ludhiana, Punjab, India. Utilizing real-world traffic video 

\[12\] A. Alahi, K. Goel, V. Ramanathan, A. Robicquet, L. Fei-Fei, and S. 

data, the research captures not only motion parameters \(such Savarese, “Social LSTM: Human trajectory prediction in crowded spaces,” in *Proceedings of the IEEE Computer Society Conference on* as speed and distance of vehicles and pedestrians\) but also *Computer Vision and Pattern Recognition*, IEEE Computer Society, contextual features like gender, age, and location on the road, Dec. 2016, pp. 961–971. doi: 10.1109/CVPR.2016.110. 

summing up to 10 different features that influence pedestrian 

\[13\] S. Zhang, M. Abdel-Aty, J. Yuan, and P. Li, “Prediction of Pedestrian Crossing Intentions at Intersections Based on Long Short-Term behavior in heterogeneous traffic. 

Memory Recurrent Neural Network,” *Transp Res Rec*, vol. 2674, no. 

The Bi-LSTM with attention model outshines the standard 4, pp. 57–65, Apr. 2020, doi: 10.1177/0361198120912422. 

LSTM in accuracy, providing more reliable predictions at 

\[14\] S. K. Jayaraman *et al. *, “Pedestrian Trust in Automated Vehicles: Role intervals ranging from 0.6 to 3 seconds into the future. The of Traffic Signal and AV Driving Behavior,” *Front Robot AI*, vol. 6, Nov. 2019, doi: 10.3389/frobt.2019.00117. 

model exhibits high recall values, crucial for safety-critical 

\[15\] Muduli, K., Sahu, D., & Ghosh, I. \(2023, July 20\). A GIS-based applications like ADAS in autonomous vehicles, ensuring framework for identification and prioritization of traffic crash hotspots. 

most pedestrians with the intention to cross are correctly Paper presented at the World Conference on Transport Research - 

identified. With over 80% accuracy at all prediction horizons, WCTR 2023, Montreal. 

\[16\] K. Muduli and I. Ghosh, “Prediction of the Future State of Pedestrians the proposed system could significantly enhance pedestrian While Jaywalking Under Non-Lane-Based Heterogeneous Traffic safety by offering earlier warnings to drivers or autonomous Conditions,” Transportation Research Record: Journal of the systems. 

Transportation Research Board, p. 036119812311616, Apr. 2023, doi: 10.1177/03611981231161619. 

The study acknowledges the complexity of pedestrian 

\[17\] A. Bochkovskiy, C.-Y. Wang, and H.-Y. M. Liao, “YOLOv4: Optimal behavior and suggests that future research should focus on Speed and Accuracy of Object Detection,” Apr. 2020, \[Online\]. 

more sophisticated deep-learning models and broader Available: http://arxiv.org/abs/2004.10934 

datasets, possibly integrating multi-modal sensor data to 

\[18\] S. Ren, K. He, R. Girshick, and J. Sun, “Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks,” *IEEE Trans* refine the accuracy and reliability of prediction systems. The *Pattern Anal Mach Intell*, vol. 39, no. 6, pp. 1137–1149, Jun. 2017, doi: proposed model could be deployed at unsignalized crossings 10.1109/TPAMI.2016.2577031. 

to facilitate I2V communication, alerting vehicles about 

\[19\] R. Girshick, “Fast R-CNN,” Apr. 2015, \[Online\]. Available: potential pedestrian 

movements, thereby preventing 

http://arxiv.org/abs/1504.08083 

\[20\] N. Wojke, A. Bewley, and D. Paulus, “Simple Online and Realtime accidents and enhancing pedestrian safety. 

Tracking with a Deep Association Metric,” Mar. 2017, \[Online\]. 



Available: http://arxiv.org/abs/1703.07402 

\[21\] N. Wojke and A. Bewley, “Deep Cosine Metric Learning for Person R

Re-Identification,” Dec. 2018, doi: 10.1109/WACV.2018.00087. 

EFERENCES 

\[22\] A. Milan, L. Leal-Taixe, I. Reid, S. Roth, and K. Schindler, “MOT16: A Benchmark for Multi-Object Tracking,” Mar. 2016, \[Online\]. 

\[1\] “Road Accidents in India Road Accidents in India Road Accidents in Available: http://arxiv.org/abs/1603.00831 

India” 2021. \[Online\]. Available: www.morth.nic.in 

\[23\] J. Jakubˇ, J. Vojtěch Bartl, and R. Juránek, “Vehicle Re-Identification 

\[2\] DTP. *Road Accidents in Delhi*. Delhi Traffic Police, Government of and Multi-Camera Tracking in Challenging City-Scale Environment.” 

Delhi, India, 2019. 

\[Online\]. Available: https://medusa.fit.vutbr.cz/traffic/ 

\[3\] CTP. *Road Accidents in Chandigarh*. Chandigarh Traffic Police, India, 

\[24\] Z. Tang *et al. *, “CityFlow: A City-Scale Benchmark for Multi-Target 2019. 

Multi-Camera Vehicle Tracking and Re-Identification,” Mar. 2019, 

\[4\] B. R. Kadali and P. Vedagiri, “Evaluation of pedestrian crossing speed 

\[Online\]. Available: http://arxiv.org/abs/1903.09254 

change patterns at unprotected mid-block crosswalks in India,” *Journal *

\[25\] N. V Chawla, K. W. Bowyer, L. O. Hall, and W. P. Kegelmeyer, *of Traffic and Transportation Engineering \(English Edition\)*, vol. 7, no. 

“SMOTE: Synthetic Minority Over-sampling Technique,” 2002. 

6, pp. 832–842, Dec. 2020, doi: 10.1016/j.jtte.2018.10.010. 



\[5\] N. N. Ferenchak, “Pedestrian age and gender in relation to crossing behavior at midblock crossings in India,” *Journal of Traffic and* *Transportation Engineering \(English Edition\)*, vol. 3, no. 4, pp. 345–

351, Aug. 2016, doi: 10.1016/j.jtte.2015.12.001. 

\[6\] “Pedestrian Crossing Behavior in Relation to Grouping and Gender in a Developing Country Context,” *Journal of Global Epidemiology and* *Environmental *

*Health*, 

pp. 

37–45, 

Dec. 

2017, 

doi: 

10.29199/geeh.101018. 

\[7\] G. Asaithambi, M. O. Kuttan, and S. Chandra, “Pedestrian Road Crossing Behavior Under Mixed Traffic Conditions: A Comparative Study of an Intersection Before and After Implementing Control Measures,” *Transportation in Developing Economies*, vol. 2, no. 2, Oct. 2016, doi: 10.1007/s40890-016-0018-5. 

\[8\] Y. Bengio, P. Simard, and P. Frasconi, “Learning Long-Term Dependencies with Gradient Descent is Difficult,” *IEEE Trans Neural* *Netw*, vol. 5, no. 2, pp. 157–166, 1994, doi: 10.1109/72.279181. 

\[9\] R. Pascanu, T. Mikolov, and Y. Bengio, “On the difficulty of training Recurrent Neural Networks,” Nov. 2012, \[Online\]. Available: http://arxiv.org/abs/1211.5063 

\[10\] M. L. , H. P. , Y. K. , J.-S. P. , G.-J. J. J.-H. K. Donghyun Lee, 

“Long\_short-term\_memory\_recurrent\_neural\_network-based\_acoustic\_model\_using\_connectionist\_temporal\_classification\_

on\_a\_large-scale\_training\_corpus”. 

\[11\] O. Ghori *et al. *, “Learning to Forecast Pedestrian Intention from Pose Dynamics,” in *IEEE Intelligent Vehicles Symposium, Proceedings*, Institute of Electrical and Electronics Engineers Inc., Oct. 2018, pp. 

1277–1284. doi: 10.1109/IVS.2018.8500657. 

209

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 12:13:22 UTC from IEEE Xplore. Restrictions apply.



