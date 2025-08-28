Transportation Research Part C 171 \(2025\) 104974 

Contents lists available at ScienceDirect

Transportation Research Part C

journal homepage: www.elsevier.com/locate/trc

Multi-agent trajectory prediction at unsignalized intersections: An 

improved generative adversarial network accounting for collision 

avoidance behaviors

Lei Zhao , Wei Zhou , Sixuan Xu , Yuzhi Chen , Chen Wang \*

*School of Transportation, Southeast University, Southeast University Road, Nanjing 211189, Jiangsu, China* A R T I C L E I N F O

A B S T R A C T

*Keywords:*

Accurate trajectory prediction for multiple agents \(i.e., vehicles, bicyclists, and pedestrians\) is the Trajectory prediction

premise of launching proactive interventions, which can serve as an effective way to improve Collision avoidance behaviors

traffic safety at unsignalized intersections. The distinctive characteristic of unsignalized in-Generative Adversarial Network

tersections lies in their disorderly traffic organization, prompting traffic agents to be extra vigilant Multi-agent

Unsignalized intersections

towards other agents to prevent collisions. As such, the primary focus of multi-agent trajectory prediction lies in acquiring a deep understanding of their interactive behavior patterns when encountering potential collisions. To achieve this, this study proposes an improved generative adversarial network \(GAN\) that can properly model collision avoidance behaviors of multiple agents when predicting their trajectories. Specifically, attention pooling modules are employed to capture interactions among multiple agents. A graph convolution network \(GCN\) based collision extraction module is applied to identify potential collisions and model the collision avoidance behaviors of traffic agents. Experimental results on *InD * dataset demonstrate that the proposed framework attained a more accurate and reliable performance for multi-agent trajectory prediction. In different interactive scenarios, such as when vehicles yield or don’t yield, the results illustrated via the Distance-velocity \(DV\) diagram display a significant level of robustness. 

Furthermore, the conflict points, count of dangerous interactions, and Post-Encroachment Time, as computed from these predicted trajectories, also align well with the ground truth. This indicates that the proposed framework effectively captures the pattern of collision avoidance behaviors of multiple agents, which has potential to serve as an effective way to enhance traffic safety at unsignalized intersections. 

**1. Introduction**

Unsignalized intersection is considered as one of the most hazardous locations in the road network since the common intersection area is shared by multiple agents \(i.e., vehicles, bicyclists, and pedestrians\), and the variety of their movements creates several collisions \(Yang et al., 2019; Zhang and Yan, 2023\). Without traffic signals regulating the right-of-way and providing clear instructions, traffic agents commonly make decisions based on their own judgement, which could be subjective and in turn increase the likelihood of accidents. 

\* Corresponding author. 

*E-mail addresses: *lei\_zhao@seu.edu.cn \(L. Zhao\), vvgod@seu.edu.cn \(W. Zhou\), 220203278@seu.edu.cn \(S. Xu\), yuzhi\_chen@seu.edu.cn

\(Y. Chen\), chen\_david\_wang@seu.edu.cn \(C. Wang\). 

https://doi.org/10.1016/j.trc.2024.104974

Received 9 October 2023; Received in revised form 19 August 2024; Accepted 12 December 2024 

Available online 6 January 2025 

0968-090X/© 2024 Elsevier Ltd. All rights are reserved, including those for text and data mining, AI training, and similar technologies. 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

To improve traffic safety at unsignalized intersections, proactive interventions have gained widespread attention and application, given their ability to effectively anticipate collision risks and promptly alert pedestrians or vehicles \(Feng et al., 2022; Høye and 

Laureshyn, 2019; Noh and Yeo, 2022\). However, the successful implementation of proactive safety warnings crucially relies on the accurate trajectory prediction of all traffic agents. Consequently, there is a pressing need for effective trajectory prediction models to serve as the foundation of proactive interventions at unsignalized intersections. 

Existing approaches for trajectory prediction primarily rely on historical trajectories, which motivate most traditional models such as Social Force approach \(Rudenko et al., 2018\), Hidden Markov Model \(Firl et al., 2012\), and Bayesian Filter \(Schneider and Gavrila, 

2013\). In addition, thanks to the excellent performance of deep learning in sequence modeling tasks such as speech recognition and machine translation, many deep-learning models including Long Short Term Memory \(LSTM\)-based \(Song et al., 2021; Zhang et al., 

2019\), Generative Adversarial Network \(GAN\)-based \(Gupta et al., 2018; Sadeghian et al., 2019\) and Graph Convolution Network \(GCN\)-based \(Shi et al., 2021; Yu et al., 2020\) are proposed for trajectory prediction. Apart from sequence information hidden in ego-trajectories, recent deep-learning models \(Kalatian and Farooq, 2022; Wang et al., 2023\) increasingly focus on socially aware information including interactions between pedestrians, the environmental constraints \(Li et al., 2023b\), etc. Specifically, methods like social pooling \(Alahi et al., 2016\) or graph attention networks \(Huang et al., 2019; Kosaraju et al., 2019; Liu et al., 2022b\) are frequently used to address these aspects. These approaches have been demonstrated to outperform most traditional models that rely solely on sequence information. 

Most existing works on trajectory prediction are customized for pedestrians or vehicles. But the problem of multi-agent trajectory prediction at unsignalized intersections has been underexplored. Factors like varying speeds and uncertain crossing behaviors of traffic agents also increase the challenges in accurately modeling their behavior patterns \(Zhang and Berger, 2023\). Consequently, com-prehending the decision-making process and interactions among multiple agents becomes essential for multi-agent trajectory prediction. Furthermore, a socially-attended attack experiment \(Saadatnejad et al., 2022\) has demonstrated that even small perturbations \(i.e., *< * 0.2 m\) in observed trajectories can lead to collisions in predicted trajectories. This experiment highlights the main limitation of data-driven models, i.e., the lack of social understanding, even when models have access to interaction information such as relative positions and relative velocities of multiple agents. This may primarily be the reason why only the sharing of positional information is not enough for models to understand the behavior patterns of different traffic agents during interactions. Generally, pedestrians and vehicles tend to avoid collisions during interactions \(as shown in Fig. 1\). Potential collisions are significant factors that need to be fully considered by all traffic agents at each time step before they make the next decision, otherwise, a traffic accident may take place. 

Therefore, emphasizing traffic agents’ collision avoidance behaviors helps the model learn how to predict. 

Based on the above, this paper explores the idea of developing a deep learning framework that can model collision avoidance behaviors of multiple traffic agents at unsignalized intersections. It is worth noting that this paper extends the scenes from one kind of agent \(i.e., pedestrians\) on streets to multiple agents \(i.e., vehicles, bicyclists, pedestrians, etc.\) at unsignalized intersections. To achieve this, an improved generative adversarial network \(GAN\) is carefully constructed. 

**Fig. 1. **Collision avoidance behaviors of traffic agents at unsignalized intersections. 

2 

*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

Generative Adversarial Network \(GAN\) is a type of deep learning network composed of a generator and a discriminator, designed to generate realistic data through adversarial training. The core idea behind GANs is to continually generate data using the generator while teaching the discriminator to distinguish between real and fake data. This process gradually enhances the generator’s ability to produce data that closely matches real ones. \(Fang et al., 2022; Pang et al., 2022; Zhou et al., 2023b\). By integrating collision avoidance behaviors into the generator, it becomes feasible to produce trajectories that can more accurately reflect the behavioral dynamics of various traffic agents. Meanwhile, the discriminator plays a crucial role in assessing these generated trajectories and filtering out those that are highly implausible. This adversarial process ensures that the resulting trajectories are not only realistic but also highly applicable, making them more reasonable in real-world traffic scenarios. 

Specifically, this paper considers the heterogeneous kinetic characteristics and interactions among multiple agents. To effectively capture these interactions, attention pooling modules are employed. Furthermore, this study takes a step forward to model the collision avoidance behaviors of traffic agents by introducing a collision extraction module. Additionally, the Distance-Velocity diagram \(Fu 

et al., 2018\) is applied to evaluate the proposed framework and to further analyze the interactions among multiple agents. In summary, the contributions of this work are as follows: 

\(1\) An improved generative adversarial network \(GAN\) is proposed to predict multi-agent trajectories simultaneously at unsignalized intersections. Collision avoidance behaviors of multiple agents are taken into consideration and further integrated with their interactions. 

\(2\) A GCN-based collision extraction module is proposed to model the collision avoidance behaviors of traffic agents. Specifically, the kernel function of the graph is defined by a two-dimensional surrogate safety indicator \(Venthuruthiyil and Chunchu, 2022; 

Xie et al., 2021\), which facilitates the agents’ collision inference process. 

\(3\) Distance-Velocity diagram is used to analyze interactions among multiple agents. The collision avoidance behaviors of multiple agents in near misses are well modeled according to trajectories generated by the model. Traffic conflict techniques \(e.g., Post-Encroachment time\) are also applied to quantify the collision risks of multiple agents. 

The rest of this paper is organized as follows: Section 2 reviews related studies in trajectory prediction and interactions among multiple agents. Section 3 introduces the methodology for constructing the generative adversarial network by each module. Section 4

evaluates the proposed model and discusses collision risks of multiple agents based on a natural driving dataset. Section 5 concludes this study and describes future extensions. 

**2. Literature review**

*2.1. Multi-agent trajectory prediction*

Accurate trajectory prediction for multiple traffic agents at unsignalized intersections is of great significance in enhancnig traffic safety. Unlike predicting trajectories for pedestrians or vehicles only, which focuses on a single agent within a specific scenario \(Geng 

et al., 2023b; Nayak et al., 2022\). Predicting trajectories for multiple agents simultaneously necessitates comprehensive consideration of the distinctions in their appearance and behaviors, making it a more challenging task. Existing multi-agent trajectory prediction methods can be roughly divided into conventional models and deep learning-based models. 

Conventional trajectory prediction models are always hand-crafted based on the input features such as historical trajectories and scene information. Social force model was generally integrated into trajectory prediction models due to its effectiveness in quantifying the influence of pedestrians on each other or from the environment \(Cao et al., 2017; Helbing and Molnar, 1995; Zhang et al., 2023b\). 

For instance, in the human motion prediction method proposed by Rudenko et al. \(2018\), social force was utilized to model local interactions with other nearby agents. Zhang et al. \(2021\) applied social force model to describe social interactions at an unsignalized crosswalk. And the recently proposed pedestrian trajectory model ForceFormer also imported social forces into a data-driven model to learn stochastic pedestrian behavior \(Zhang et al., 2023b\). Kinematic models, such as Kalman filter \(Keller et al., 2011\) and the constant turn rate and acceleration \(CTRA\) model \(Schubert et al., 2008\), offer another effective approach for trajectory prediction. 

However, their dependence on historical trajectories may restrict their accuracy in complex scenarios. To overcome this limitation, Ju 

et al. \(2020\) proposed a multi-layer architecture called Interaction-aware Kalman Neural Networks \(IaKNN\) that incorporates dynamic and interaction-aware trajectories to improve prediction performance. Additionally, Xie et al. \(2018\) integrated physics-based and maneuver-based approaches, while Malviya and Kala \(2022\) combined the social force model with the particle filter. These integrated models have demonstrated improved performance compared to traditional trajectory prediction models. 

Deep learning-based models mainly rely on social pooling, attention mechanism, and graph neural networks to model interactions among multiple agents. For instance, Deo and Trivedi \(2018\) proposed convolutional social pooling. Bi et al. \(2019\) introduced Vehicle-Pedestrian LSTM \(VP-LSTM\) which incorporates mixed social pooling. Furthermore, attention mechanism is also commonly used to address the interactions among multiple agents. Huang et al. \(2021\) employed a focal attention mechanism to address the interactions between pedestrians, cyclists, and vehicles. Amirloo et al. \(2022\) applied a hierarchical attention mechanism to exploit the future states of multiple agents. More commonly, attention mechanism is combined with graph neural networks to construct graph attention networks \(Li et al., 2022a; Mo et al., 2022; Zhang et al., 2022; Zhou et al., 2023a\). Salzmann et al. \(2020\) introduced Trajectron\+\+, a widely used graph structured recurrent model with an additive attention module for multi-agent behavior prediction. 

Targeting autonomous driving, Shi et al. \(2023b\) proposed Motion TRansformer \(MTR\+\+\) framework, which achieved outstanding performance on the famous Waymo Open Motion Dataset \(WOMD\). Lan et al. \(2023\) proposed Scene Encoding Predictive Transformer 3 

*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

\(SEPT\) and tested it on the Argoverse dataset. 

Although many existing methods have considered interactions among multiple agents, the social understanding of these models has not been fully exploited. As pointed out by Saadatnejad et al. \(2022\), a small disturbance to the observed trajectory could lead to significant prediction errors, highlighting the need to improve social understanding of deep learning based-models. In more recent studies, Pang et al. \(2022\) proposed a novel behavior recognition module to obtain extra pedestrian behavior information by embedding the behavior label of standing, moving and grouping. Additionally, Zhang and Li \(2022\) focused on the explainability of trajectory prediction models, proposing a Multimodal Trajectory Prediction Transformer \(MTPT\) model to reveal the intrinsic mechanism of trajectory prediction. Liu et al. \(2022a\) constructed a driving risk map to achieve a unified representation of interactions among multiple agents in the scene. Shi et al. \(2023a\) unified the components of pedestrian trajectory prediction, such as social interaction and multimodal trajectory prediction, into a transformer encoder-decoder architecture called Trajectory Unified Transformer \(TUTR\). Therefore, considering that pedestrians and vehicles tend to avoid collisions during interactions, this paper explores the idea of integrating collision avoidance behaviors of traffic agents into deep learning models for multi-agent trajectory prediction. 

*2.2. Interactions among multiple agents*

At unsignalized intersections, interactions among multiple agents are more complex, including numerous conflicts with the potential to lead to collisions. As such, the application of traffic conflict techniques allows for the evaluation of safety risks associated with predicted trajectories, thus facilitating effective risk warnings \(Wang et al., 2021; Wang et al., 2019\). Additionally, modeling the behavior of traffic agents in near misses provides deeper insights into their behavior patterns when facing conflict risks, such as their collision avoidance behaviors. This not only enriches the social understanding of trajectory prediction models but also contributes to more accurate trajectory predictions. 

In the work of \(Zhang and Abdel-Aty, 2022; Zhang et al., 2020\), traffic conflicts between pedestrians and vehicles were divided into three categories \(i.e., severe conflicts, slight conflicts, and no conflicts\) based on indicators of Surrogate Safety Measures \(SSM\) such as Post-Encroachment Time \(PET\), Time to Collision \(TTC\), Gap Time \(GT\), etc. Deep learning-based models such as LSTM and GRU were further applied to predict pedestrian-vehicle conflicts. Chen et al. \(2017\) introduced PET and Relative Time to Collision \(RTTC\) to represent temporal and spatial proximity between pedestrians and vehicles. Zhou et al. \(2020\) estimated vehicle–pedestrian collision probability at intersections based on real-time trajectories and movement parameters \(e.g., position, velocity, acceleration or direc-tion\) of vehicles and pedestrians. While Chen et al. \(2020\) applied a spatial surrogate measure called safety space as a spatial filter to determine conflicts in mixed traffic flows. To assess the severity levels of traffic conflicts between pedestrians and vehicles, a conflict risk evaluation model considering complex interactions between motorized vehicles and pedestrians was developed \(Ezzati Amini 

et al., 2022\). Similarly, Govinda et al. \(2022\) investigated Threshold risk indicator \(RI\) values for severe pedestrian-vehicle conflicts using both pedestrian and vehicle kinetic characteristics. 

Modeling the behavior of multiple agents in near misses helps to understand their behavior patterns, thus to identify potential collisions more accurately. Yao et al. \(2021\) proposed a deep-learning framework that focuses on modeling vehicle turning behavior at mixed-flow intersections, specifically addressing diagonal-crossing motorcycle conflicts. Besides, state-space models such as Markov Decision Process \(MDP\) can be used to model traffic agents’ interactions by modeling them as intelligent agents that interact with the environment and make rational decisions to meet their objectives. Furthermore, Reinforcement Learning \(RL\) is often implemented to estimate the reward function. For example, Nasernejad et al. \(2021\) implemented a continuous Gaussian Process Inverse Reinforcement Learning \(GP-IRL\) approach to model pedestrian behavior in pedestrian-vehicle near misses. Lanzaro et al. \(2022\) proposed a deep reinforcement learning-based framework for modeling interactions between motorcyclists and pedestrians. Zhang et al. \(2023a\)

also applied a deep reinforcement learning solution methodology to find the best driving policy for autonomous vehicles. Focusing on pedestrian safety at non-signalized intersections, surrogate safety measures and Distance-Velocity \(DV\) diagram \(Fu et al., 2018\) were applied to investigate secondary pedestrian-vehicle interactions \(Fu et al., 2019\). Noh and Yeo \(2022\) used a non-parametric statistical inference method to estimate the probability distribution of the predicted trajectory, based on which the collision risk of pedestrians and vehicles can be evaluated. 

In this paper, following the work of \(Fu et al., 2019\), surrogate safety measures and Distance-Velocity \(DV\) diagram are introduced to analyze the interactions among multiple agents in near misses based on trajectories generated by the trajectory prediction model. 

Additionally, metrics such as the displacement error at conflict points are calculated to further evaluate the effectiveness of the proposed model. 

**3. Methodology**

*3.1. Problem definition*

In previous studies, the physical size of multiple agents has not been given much emphasis. However, while pedestrians and bicyclists can be regarded as particles, it is more reasonable to consider vehicles as rigid bodies with geometric dimensions. Therefore, in this paper, pedestrians and bicycles are both treated as particles, denoted as Vulnerable Road Users \(VRUs\) hereafter. In contrast, vehicles are considered as rigid non-particle objects, represented by the four vertices of an oriented bounding box \(OBB\). \(Bi et al., 

2019\). 

Then, at an unsignalized intersection where *N * VRUs and *M * vehicles are included. The trajectory of VRU *pi*\( *i *∈ \[1 *, N*\]\) is represented 4 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

\(

\)

\(

\)

by his/her position *pti *= *xti,yti *. And the position of vehicle *vi*\( *i *∈ \[1 *, M*\]\) at time *t * can be represented by *vti *= *vtfl*

, where 

*,i,vtfr,i,vtbl,i,vtbr,i*

\(

\)

*vt*\*

*xt*

*, *\* ∈ \( *fl,fr, bl,br*\). Note that given a specific vehicle with width *w * and length *l*, an OBB can also be represented by a 4 

*,i *=

\* *,i, yt*\* *,i*

\(

\)

\(

\)

dimension position *vti *= *oti, sti *= *xto*

, where *ot*

*,i, yto,i, xts,i, yts,i*

*i , sti * are the central point and precentral point of the OBB respectively. To accurately describe the interactions among multiple agents in complex scenes, historical velocities of VRUs and vehicles are also \(

\)

\(

\)

extracted and represented as ˙ *pti *= ˙ *xti, *˙ *yti * and ˙ *vti *= ˙ *xto*

, respectively. 

*,i, *˙

*yto,i*

Thus, the task of trajectory prediction is to predict future trajectories of all traffic agents given their historical trajectories, which 

\{\(

\)

\}

\{\(

\)

\}

can be defined as ̂ *pti *= ̂ *xti, *̂ *yti *| *t *= *tobs *\+1 *, *⋯ *, tpred *∀ *i *∈ \[1 *, N*\] for VRUs and ̂ *vti *= ̂ *xto*

| *t *= *t*

∀ *i *∈ \[1 *, M*\] for 

*,i, *̂

*yto,i, *̂ *xts,i, *̂ *yts,i*

*obs *\+1 *, *⋯ *, tpred*

vehicles. 

*3.2. Overall framework*

The overall framework, as illustrated in Fig. 2, is based on a generative adversarial network consisting of a generator and a discriminator. The generator leverages historical sequence information from multiple agents and Gaussian noises to generate predicted trajectories. Meanwhile, the discriminator assesses the authenticity of the generated trajectories by comparing them with real ones. 

Through continuous iterations of the generator and the discriminator, more realistic trajectories can be obtained. 

The proposed generator in our framework is comprised of four main components: an LSTM-based trajectory encoder, an LSTM-based decoder, a GCN-based collision extraction module, and attention pooling modules. The generator begins with an LSTM-based trajectory encoder that processes the historical trajectories of multiple agents, encoding them into hidden state vectors that capture the kinetic characteristics of these trajectories. Next, attention-based pooling modules are utilized to further process these vectors, incorporating real-time interaction data such as the relative positions and velocities of the agents. Following this, a GCN-based collision extraction module is employed to identify and extract collision avoidance behaviors of multiple agents. In the final step, the decoder combines these feature vectors with Gaussian noise to generate the output. 

The discriminator consists of an LSTM-based encoder and an MLP-based classifier. The role of the encoder is similar to that in the generator, which encodes the trajectory sequence. The difference is that the complete trajectory \(i.e., the observed sequence and the predicted/ground truth sequence\) is encoded in the discriminator. The classifier then evaluates whether the input trajectories are true or false, thus prompting the generator to enhance its output and produce more realistic trajectories. 

In the following subsections, we elaborate on each module in detail. 

*3.3. LSTM-based trajectory encoder*

Following the work of \(Gupta et al., 2018; Huang et al., 2019; Liu et al., 2020\), the displacements of historical trajectories are firstly calculated: 

**Fig. 2. **An illustration of the overall framework. The ***VRU*****- *VRU***, ***V**ehicle*- ***V**ehicle*, and ***VRU*****- *V****ehicle * interactions are captured by attention pooling modules. Potential collisions are identified using a collision extraction module. To generate multiple trajectories, a Gaussian noise is incorporated into the framework. 

5 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

\(

\)

\(

\)

Δ *pti *= Δ *xti, * Δ *yti *= *xti *− *xt*− 1

*i*

*, yti *− *yt*− 1

*i*

\(

\)

\(

\)

\(1\) 

Δ *vt*\*

Δ *xt*

= *xt*

*, *\* ∈ \( *fl, fr, bl, br*\)

*,i *=

\* *,i, * Δ *yt*\* *,i*

\* *,i *− *xt*− 1

\* *,i , yt*\* *,i *− *yt*− 1

\* *,i*

Where Δ *pti * and Δ *vt*\* *,i * are the displacements of *VRUs * and vehicles, respectively. Then Δ *pti * and Δ *vt*\* *,i * are fed into an embedding layer, which is shown as follows: 

\(

\)

*ep,ti *= *ϕ * Δ *pti*; *Wp*

\(

\)

*ev*\* *,t*

*i*

= *ϕ * Δ *vt*\*

*, *\* ∈ \( *fl, fr, bl, br*\)

*,i*; *Wv*\*

\(2\) 

\(

\)

*ev,ti *= *ϕ evfl,t*

*i , evfr,t*

*i*

*, evbl,t*

*i*

*, evbr,t*

*i*

; *Wv*

Where *ϕ*\(\) is an embedding function with PRELU nonlinearity, *Wp * is weights for *VRUs*, and *Wv , W*

\*

*v * are the weights for vehicles. 

Finally, an LSTM layer is applied to encode the embedding vector *ep,t*

*i *, *ev*\* *,t*

*i *

to obtain the hidden states: 

\(

\)

*hp,tei *= *LSTM hp,t*− 1

*ei*

*, ep,t*

*i *; *Wencoder,p*

\(

\)

\(3\) 

*hv,tei *= *LSTM hv,t*− 1

*ei*

*, ev,t*

*i *; *Wencoder,v*

*3.4. Attention pooling modules for multi-agent interactions*

In addition to sequence information hidden in historical trajectories, interactions among multiple agents also have a significant impact on their future trajectories. 

For instance, the yielding behavior of vehicles may prompt VRUs to hasten their pace to cross the crosswalk. Besides, VRU *s * and vehicles behave differently while interacting with other agents \(Cheng and Sester, 2018\). Pedestrians, in particular, tend to move slowly and flexibly, often gathering together while interacting with other pedestrians. In contrast, vehicles typically move quickly and maintain a considerable distance when interacting with pedestrians. To capture these differences, this paper models three different interactions of ***VRU***- ***VRU***, ***V**ehicle*- ***V**ehicle*, and ***VRU***- ***V**ehicle * separately. Additionally, attention mechanism is introduced to extract differentiated interactive features. This process is illustrated in Fig. 3. 

The inputs of attention pooling modules are defined as *RItij * and *R*˙ *Itij*, where *I *= \{ *P, V, PV*\} to represent the relative position and relative velocity for ***VRU***- ***VRU***, ***V**ehicle*- ***V**ehicle*, and ***VRU***- ***V**ehicle. *

*3.4.1. **VRU**-**VRU***

The interaction features between VRUs are extracted by an attention pooling module. First, relative position *RPtij * and relative velocity *R *˙ *Ptij * between *pi * and *pj*\( *i, j *∈ \[1 *, N*\]\) are calculated and fed into a fully connected layer for encoding. Subsequently, an MLP with **Fig. 3. **Attention pooling modules for multi-agent interactions. 

6 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

softmax activation function is used to calculate the attention weight of VRUs to other agents in the scene \(including vehicles and other VRUs\). The hidden state vector \(i.e., after LSTM encoding\) of the target VRU is then combined with the ***VRU***- ***VRU *** interaction encoding vector using another MLP. Finally, the attention-weighted vector is obtained through max pooling. 

\(

\)

*ep*− *p,t*

*ij*

= *ϕ RPtij, R *˙ *Ptij*; *Wembedding*

\(4\) 

*,pp*

\( \(

\)\)

*αpp,t*

*i*

*φ RPt*

\(5\) 

*,j , αpv,t*

*i,j *= *softmax*

*ij, R *˙

*Ptij, RPVtij, R *˙ *PVtij*; *Wattention,p*

\(

\(

\)\)

*hp*− *p,t*

*i*

= *maxpool αpp,t*

*i*

*hp,t*

\(6\) 

*,j*

× *φ*

*ei , ep*− *p,t*

*ij*

; *Wmlp,pp*

*3.4.2. **V**ehicle-**V**ehicle*

To model the interaction between vehicles, we consider the input to be relative position and relative velocity of the two coordinate points: the OBB center point and the front center point. Specifically, the relative position *RVtij * and relative velocity *R *˙ *Vtij * between vehicle *vi * and *vj*\( *j *∈ \[1 *, M*\]\) are also sent to a fully connected layer. After the attention pooling module, MLP encoding module, and max pooling module, the hidden vector representing ***V**ehicle*- ***V**ehicle * interaction is obtained. 

\(

\)

*ev*− *v,t*

*ij*

= *ϕ RVtij, R *˙ *Vtij*; *Wembedding*

\(7\) 

*,vv*

\( \(

\)\)

*αvv,t*

*i*

*φ RVt*

\(8\) 

*,j , αvp,t*

*i,j *= *softmax*

*ij, R *˙

*Vtij, RPVtij, R *˙ *PVtij*; *Wattention,v*

\(

\(

\)\)

*hv*− *v,t*

*i*

= *maxpool αvv,t*

*i*

*hv,t*

\(9\) 

*,j*

× *φ*

*ei , ev*− *v,t*

*ij*

; *Wmlp,vv*

*3.4.3. **VRU**-**V**ehicle*

Compared to the ***VRU***- ***VRU *** and ***V**ehicle*- ***V**ehicle * interactions, the interactions between *VRUs * and vehicles are more complex due to their behavioral differences. For instance, vehicles tend to maintain a larger distance and lower speed to avoid colliding with VRUs, while VRUs \(especially pedestrians\) tend to hold a smaller distance from others when crossing the street due to their flexibility and wide field of vision. Additionally, pedestrians’ crossing speed may change more frequently, especially when vehicles yield to them. To capture these behavioral differences in the ***VRU***- ***V**ehicle * interaction, relative position as well as relative velocity between VRUs and vehicles are encoded. Similarly, after the MLP encoding module and max pooling module, the hidden vector *hp*− *v,t* *i*

*, hv*− *p,t*

*i *

representing 

their interactions are obtained. 

\(

\)

*ep*− *v,t*

*ij*

= *ϕ RPVtij, R *˙ *PVtij*; *Wembedding*

\(10\) 

*,pv*

\(\{

\}

\(

\)\)

*hp*− *v,t*

*i*

*, hv*− *p,t*

*i*

= *maxpool*

*αpv,t*

*i*

× *φ hp,t*

\(11\) 

*,j , αvp,t*

*i,j*

*ei , hv,t*

*ei , ep*− *v,t*

*ij*

; *Wmlp,pv*

**Fig. 4. **GCN-based collision extraction module. 

7 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

*3.5. GCN-based collision extraction module*

Although attention pooling modules have fully considered the interactions among multiple agents such as relative velocity, relative position, etc. The social understanding to their interactions has not been fully exploited. The pooling modules only serve as roles to converge those fragmented information into hidden vectors that can be globally shared. However, for multiple agents, there is an inference process from the acquisition of shared information to the generation of future trajectories. This process may help models gain a deep understanding of their behavior patterns, which is lacking in existing trajectory prediction models \(Saadatnejad et al., 2022\). 

Given that in the interaction process among multiple agents, VRUs and vehicles will infer the risk of collisions based on the obtained shared information and then generate the next behavior. This paper introduced a GCN-based collision extraction module to address this problem. Specifically, the relationships among multiple agents at unsignalized intersections are initially represented using a graph structure. Then, the agents’ inference process of the collision risk is characterized by a two-dimensional surrogate safety indicator 

\(Venthuruthiyil and Chunchu, 2022; Xie et al., 2021\), based on which the adjacency matrix is constructed. Finally, spatio-temporal graph convolution operations are applied to extract the collision avoidance behaviors of multiple agents. This process is shown in 

Fig. 4. 

*3.5.1. Graph representation*

To begin with, a graph is constructed to represent the relationships among multiple agents. This graph is defined as *Gt *= \(**V ** *t, ***E ** *t*\) at time step *t*, where **V ** *t * denotes the set of vertices in *Gt*, and **E ** *t * represents the set of edges in *Gt*. The attributes of **V ** *t * include the \(

\)

\(

\)

\{ ⃒

positions and velocities of multiple agents. For VRUs, *t*

*t*

*t*

⃒

**V ** *i *= *xti, yti, *˙ *xti, *˙ *yti *, and for vehicles, **V ** *i *= *xto*

. 

*et *⃒∀ *i, *

*,i, yto,i, *˙

*xto,i, *˙ *yto,i ***E ** *ij *= *ij*

\}

*j *∈ \{1 *, *⋯ *, N *\+ *M*\} represent the connections between *t* *t*

*t*

*t*

**V ** *i * and **V ** *j*. If **V ** *i * and **V ** *j * are connected, *etij *= 1, otherwise, *etij *= 0. Moreover, 

\{

\}

an adjacency matrix *At *= *aijt*|∀ *i, j *∈\{1 *, *⋯ *, N *\+ *M*\} is calculated by a kernel function that considers the anticipated collision time of *t*

*t*

**V ** *i * and **V ** *j*. The kernel function *aijt * is defined as follows \(Venthuruthiyil and Chunchu, 2022; Xie et al., 2021\): 

⃒

⃒

̅→ *ij*

̅→ *ij*

̅→ *ij*

⃒

⃒

Δ *d*

⃒ Δ *d t *⃒ *cosα*

*ξij*

*t *• Δ *v t*

*t *=

⃒

⃒

⃒

⃒

\(12\) 

⃒̅→ *ij*⃒2

=

⃒̅→ *ij*⃒

⃒ Δ *v*

⃒ Δ *v *⃒

*t *⃒

*t*

\{ ⃒ ⃒

⃒ ⃒

*tij*

*ξijt , ξijt < * 0

*c *=

\(13\) 

\+∞ *, ξijt *≥ 0

*aij*

1

*t *= *ajit *=

\(14\) 

*tijc*

\(

\)

\(

\)

Where ̅→ *ij*

̅→ *ij*

̅→ *ij*

̅→ *ij*

Δ *d t *= *xit *− *xjt,yit *− *yjt *, Δ *v t *= ˙ *xit *− ˙ *xjt, *˙ *yit *− ˙ *yjt *, *α * represents the angle between Δ *d t * and Δ *v t *. In fact, *ξijt * represents the **Fig. 5. **The representation of potential collisions. \(a\) A negative ***ξijt *** indicates the presence of potential collisions between agent ***i *** and ***j***. \(b\) Conversely, no collisions are presented. 

8 

*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

⃒

⃒

ratio of the projection of ̅→ *ij*

̅→ *ij*

⃒̅→ *ij*⃒

Δ *d t * on Δ *v t * to ⃒ Δ *v t *⃒ \(as shown in Fig. 5\). 

It is important to note that only a negative value of *ξijt * indicates the presence of potential collisions, and the absolute value of *ξijt* denotes the anticipated collision time. Conversely, if *ξijt *≥ 0, no collisions are presented, and the anticipated collision time, *tijc*, is considered to be infinite \( \+ ∞\). 

Intuitively, the smaller the *tijc*, the greater the closeness of time and space between agent *i * and *j*, which means that it may cause a greater risk of collisions. Therefore, the closeness of the relationship between agent *i * and *j * in graph *Gt * represents the agent’s inference process for potential collision risks. 

*3.5.2. Spatio-temporal graph convolution*

The graph convolution operation is applied on graph Gt = \(**V **t *, ***E **t\): 

⎛

⎞

∑

\(

\)

\(

\)

*l*

1

\+1

⎜

*l*

*l*

*l*

*l *⎟

**V ** *i*

= *σ*⎝

*p ***V**

*.W ***V**

⎠

\(15\) 

Ω

*i, ***V ** *j*

*i, ***V ** *j*

*l*

*l*

**V ** *j*∈ *B*\(**V ** *i*\)

\(

\)

\(

\)

Where 1 */* Ω is a normalization term, B

*l*

*l*

*l*

*l*

**V ** *i * is the neighbor nodes set of **V ** *i * and *l * is the convolutional layer, *p ***V ** *i, ***V ** *j * denotes the shortest path connecting agent *i * and *j * according to the weights defined by the adjacency matrix. σ represents the activation function \(

\)

and *W*

*l*

*l*

**V ** *i, ***V ** *j * is trainable parameter at layer *l*. Interested readers are referred to \(Yan et al., 2018\) for more detailed explanations and reasoning. Then the adjacency matrix *At * is normalized using the following equation: 1

1

̂

*A*

− 2

− 2

*t *= Λ *t *\( *At *\+ *I*\)Λ *t*

\(16\) 

Where 

∑

Λ *t *=

\( *At *\+ *I*\), and *I * represented the identity matrix. Then the convolution operation to the graph representation is defined as follows: 

\(

\)

*ht,l*\+1

̂

*i*

= *σ Ah*\( *t,l*\)

*i*

*W*\( *l*\)

\(17\) 

After the application of spatio-temporal graph convolution, the hidden states representing collision avoidance behaviors for multiple agents can be obtained, which are denoted as *hp,t,l*

*i *

and *hv,t,l*

*i *

respectively. 

*3.6. LSTM-based trajectory decoder*

After the attention pooling module for multi-agent interactions representation and the GCN-based collision extraction module for collision avoidance behavior representation, the hidden states for VRUs \(i.e., *hp*− *p,t* *i*

*, hp*− *v,t*

*i*

*, hp,t,l*

*i*

\) and vehicles \(i.e., *hv*− *v,t*

*i*

*, hv*− *p,t*

*i*

*, hv,t,l*

*i *\) are 

combined using an MLP. The aggregated vector is then merged with a Gaussian noise variable *z*, which enables the generation of multiple possible outcomes. 

\(

\)

*Cp,ti *= *φ hp*− *p,t*

*i*

*, hp*− *v,t*

*i*

*, hp,t,l*

*i*

; *Wmlp,p*

\(

\)

\(18\) 

*Cv,ti *= *φ hv*− *v,t*

*i*

*, hv*− *p,t*

*i*

*, hv,t,l*

*i *; *Wmlp,v*

\[

\]

*hp,t*− 1

*di*

= *Cp,t*− 1

*i*

*, z*

\[

\]

\(19\) 

*hv,t*− 1

*di*

= *Cv,t*− 1

*i*

*, z*

After that, the hidden vector *hp,t*− 1

*di*

\( *hv,t*− 1

*di*

\) at time *t *− 1 and the encoded coordinate vector *ep,tdi*\( *ev,tdi*\) at time *t * are fed into an LSTM-based trajectory decoder. 

\(

\)

*ep,tdi *= *ϕ * Δ̂ *pt*− 1

*i*

; *W* ˆ *p*

\(

\)

\(20\) 

*ev,tdi *= *ϕ * Δ̂ *vt*− 1

*i*

; *W* ˆ *v*

\(

\)

*hp,tdi *= *LSTM hp,t*− 1

*di*

*, ep,t*

*di *; *Wdecoder,p*

\(

\)

\(21\) 

*hv,tdi *= *LSTM hv,t*− 1

*di*

*, ev,t*

*di *; *Wdecoder,v*

Finally, the displacements of VRUs Δ̂ *pti * and vehicles Δ̂ *vti * can be predicted by another MLP, which is defined as follows: \(

\)

\(

\)

Δ̂

*pti *= Δ̂ *xti, * Δ̂ *yti *= *φ hp,tdi*; *Woutput,p*

\(

\)

\(

\)

\(

\)

\(22\) 

Δ̂

*vti *= Δ̂ *oti, * Δ̂ *sti *= Δ̂ *xto*

= *φ hp,t*

*,i, * Δ̂

*yto,i, * Δ̂ *xts,i, * Δ̂ *yts,i*

*di *; *Woutput,v*

9 

*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

*3.7. Discriminator and losses*

The predicted trajectory *trpred * and the ground truth trajectory *trtruth * are concatenated with the observed trajectory *trobs * to form the 

\[

\]

input for the discriminator. Specifically, the ‘Fake’ trajectory *trobs, trpred * generated by the generator and the ‘True’ trajectory \[ *trobs, *

\{\[

\]

\}

*trtruth*\] obtained from the ground truth are combined to form a set *T *= *trobs, trpred , *\[ *trobs, trtruth*\] . 

Then the input trajectories are embedded by a fully connected layer and an LSTM layer. After that, a classifier defined by an MLP is applied to judge the authenticity of the trajectories by comparing the generated trajectories with real ones. 

The losses of the proposed model are composed of two parts: the *L* 2 loss, which denotes the position displacement loss, and the adversarial loss *LGAN*, which denotes the loss of GAN framework. 

*L* 2 = *mink*‖̂ *Yki *− *Yi*‖2

\(23\) 

*LGAN*\( *G, D*\) = *minGmaxD* E *x pdata*\( *x*\)\[ *logD*\( *x*\) \] \+ E *z p*\( *z*\)\[ *log*\(1 − *D*\( *G*\( *z*\) \) \) \]

\(24\) 

Therefore, the total loss function of the proposed model can be expressed as follows: 

*L *= *λL* 2 \+ *LGAN*\( *G, D*\)

\(25\) 

**4. Experiments**

*4.1. Dataset and data pre-processing*

The proposed framework is evaluated on *InD * dataset, which is a large-scale urban intersection dataset containing trajectories of 13,599 road users, including cars, trucks, buses, pedestrians, and bicyclists. The dataset consists of 34 recordings covering four unsignalized intersections, and each recording contains a video with a frame rate of 25 and a duration of approximately 20–22 min. 

More details about the dataset and relevant research can be found in \(Bertugli et al., 2021; Bock et al., 2020; Chen et al., 2021; Geng 

et al., 2023a\). 

In our experiments, trajectories that remain stationary or have a very short duration are excluded, as these do not contribute significantly to the prediction task. For each recording, fields such as the agent’s position, velocity, orientation, category, length, and width are extracted. After downsampling, the trajectories of multiple agents are obtained, which are then used to predict their future trajectories simultaneously, with a particular focus on outputting vehicle trajectories in the form of Oriented Bounding Boxes \(OBB\). 

For dataset division, the recordings for each intersection in the *InD * dataset are split into training and testing sets in an 8:2 ratio. In addition, for each trajectory sequence, following the research of \(Alahi et al., 2016; Gupta et al., 2018\), the first 8 sequences \(3.2 s\) are used as observed sequences, while the last 12 sequences \(4.8 s\) are used as predicted sequences. 

*4.2. Evaluation metrics*

Following previous works \(Gupta et al., 2018; Sadeghian et al., 2019; Zhang and Li, 2022\),  ***ADE *** and ***FDE *** can be defined as follows: **Average Displacement Error \(ADE\): **The average Euclidean distance between the ground truth and the predicted trajectories of all predicted time steps. 

∑ *N *∑

\+ *M*

*tpred*

*ADE*

*i*

*t*

=

=1

= *tobs*\+1‖ ̂

*Yti *− *Yti*‖2

\(

\)

\(26\) 

\( *N *\+ *M*\) *tpred *− *tobs*

**Final Displacement Error \(FDE\): **Euclidean distance between the ground truth and the predicted position at the final time step. 

∑ *N*\+ *M*

*FDE *= *i*=1 ‖̂ *Ytpred*

*i*

− *Ytpred*

*i*

‖2

*N *\+ *M*

\(27\) 

Since the models could output multiple trajectories and take the best one as the final prediction, the ADE and FDE between the best-predicted trajectory and the ground-truth trajectory can be defined as ***minADE *** and ***minFDE***. Therefore, ***minADE *** and ***minFDE *** are applied in this study as the metrics to evaluate the performance of the proposed models. 

Besides, ***minADEO *** and ***minFDEO ***\(Bi et al., 2019; Yao et al., 2021\) are used to describe the errors between predicted orientations and ground truth orientations for vehicles. 

*4.3. Implementation details*

Following the work of Social-GAN \(Gupta et al., 2018\), the parameters used in this work are fine-tuned to fit the framework proposed in this paper. Specifically, the embedding dimensions for VRUs and vehicles are set to 16 and 32, respectively. In the generator, the dimensions of the LSTM-Encoder for VRUs and vehicles are both set to 32, and the dimensions of the decoder are set to 32 and 64, respectively. In the discriminator, the encoder and decoder dimensions are both set to 64 for VRUs and vehicles. The noise dimension is set to 8. In the attention pooling modules, the MLP dimensions of all layers are set to 64. In the collision extraction module, only 1 layer of spatio-temporal graph is applied, with a kernel size of 3. Except for the attention pooling modules, which use 10 

*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

the softmax activation function, all other activation functions are set to PRELU. The Adam optimizer is used with a learning rate of 0.00001. After 300 epochs of training, the generator is used to generate 20 samples. 

*4.4. Trajectory prediction results*

*4.4.1. Models for comparison*

To evaluate the performance of the proposed framework, the following models are used as baselines. 

**VP-LSTM \(**Bi et al., 2019**\): **a vehicle–pedestrian trajectory prediction method based on LSTM, where vehicles and pedestrians are treated as rigid bodies and particles, respectively. 

**Trajectronþþ \(**Salzmann et al., 2020**\): **a generative trajectory prediction method, which can incorporate heterogeneous data beyond prior trajectory information and can produce future-conditional predictions that respect dynamics constraints. 

**Multiclass-SGCN \(**Li et al., 2022b**\): **a multi-class trajectory prediction framework that takes into consideration velocity and agent label information, which is based on a sparse graph convolution network. 

**TUTR \(**Shi et al., 2023a**\): **a trajectory-unified Transformer framework, which unifies the social interaction and multimodal trajectory prediction into an encoder-decoder transformer architecture. 

The complete framework proposed in this paper is referred as **MACA-GAN **\(multi-agent trajectory prediction based on generative adversarial networks accounting for collision avoidance behaviors\). And the framework without collision extraction module is named **MA-GAN**, which is also used for comparison. 

*4.4.2. Results of predicted trajectories*

The *minADE * and *minFDE * for different models are presented in Table 1. For VRUs’ trajectory prediction, both TUTR and MACA-GAN 

have shown excellent performance, with their *minADE * hovering around 0.5. Comparatively, MACA-GAN demonstrates superior performance. For vehicles’ trajectory prediction, our proposed models, MA-GAN and MACA-GAN, significantly improve prediction performance across all four intersections in the dataset. Both models showcase accurate predictions of vehicle positions and orientations. Furthermore, with the collision extraction module that considers potential collisions among multiple agents, MACA-GAN 

achieves the lowest average *minADE * and *minFDE*, which highlights the model’s superiority in VRUs’ trajectory prediction, vehicles’ 

trajectory prediction, and average performance. 

Additionally, Table 1 reveals that our proposed model performs exceptionally well at the *Frankenburg * and *Bendplatz, * which are both four-arm intersections. However, at the two T-junctions \( *Neukollner Strasse * and *Heckstrasse*\), the predictive performance is somewhat lower, with some metrics \(e.g., *minADE * for VRUs\) even falling behind those of comparison models like TUTR. The enhanced performance of MACA-GAN at the four-arm intersections can be attributed to several factors. Primarily, the datasets for the *Frankenburg* and *Bendplatz * intersections are more extensive and feature a more balanced distribution of VRU and vehicle trajectories, facilitating more effective model training. Furthermore, our proposed model is specifically designed for unsignalized intersections with mixed traffic agents. It incorporates attention pooling modules to capture ***VRU-VRU***, ***V**ehicle-**V**ehicle*, and ***VRU**-**V**ehicl* e interactions, as well as a GCN-based collision extraction module focused on multi-agent collision avoidance behaviors. Consequently, the model exhibits superior performance in scenarios characterized by frequent multi-agent interactions, such as vehicle turning and pedestrian crossing, which are prevalent in four-arm intersections. 

**Table 1 **

The *minADE * and *minFDE * of predicted trajectories \(in meters\). 

Location

Agent

Trajectron\+\+

Multiclass-SGCN

TUTR

VP-LSTM

MA-GAN

MACA-GAN

*Neukollner Strasse*

VRUs

0.76 / 1.50

0.63 / 1.48

0.48 / 1.09

1.01 / 2.30

0.35 / **0.61**

**0.32 / **0.64

Vehicles a

1.55 / 3.52

2.03 / 5.06

**1.11 **/ 2.74

3.28 / 8.80 

1.54 / 3.00 

1.12 / **1.88 **

3.49 / 9.07

1.62 / 3.11

1.15 / 2.18

Average b

1.10 / 2.38

1.24 / 3.03

0.75 / 1.80

1.99 / 5.11

0.86 / 1.64

**0.66 / 1.17**

*Bendplatz*

VRUs

0.61 / 1.24

0.59 / 1.36

0.46 / 1.03

0.92 / 2.08

0.32 / **0.56**

**0.29 **/ 0.63

Vehicles

1.30 / 3.10

1.66 / 4.33

0.69 / 1.79

2.78 / 7.15 

0.80 / 1.90 

**0.68 / 1.60 **

2.98 / 7.50

0.91 / 2.13

0.85 / 1.87

Average

0.92 / 2.06

1.06 / 2.67

0.56 / 1.36

1.74 / 4.31

0.53 / 1.15

**0.46 / 1.06**

*Frankenburg*

VRUs

0.65 / 1.36

0.73 / 1.55

**0.50 **/ 1.12

1.13 / 2.60

0.61 / **1.01**

0.52 / 1.04

Vehicles

1.19 / 2.98

1.60 / 3.74

0.82 / 1.91

2.53 / 6.31 

0.82 / 1.69 

**0.74 / 1.55 **

2.87 / 6.72

0.91 / 1.86

0.81 / 1.70

Average

0.79 / 1.79

0.96 / 2.12

0.59 / 1.32

1.52 / 3.58

0.66 / 1.19

**0.57 / 1.17**

*Heckstrasse*

VRUs

0.73 / 1.41

0.69 / 1.48

**0.38 / 0.85**

0.64 / 1.43

0.60 / 1.15

0.55 / 1.04

Vehicles

1.30 / 2.67

2.26 / 5.30

1.05 / 2.57

2.51 / 6.00 

1.37 / 2.98 

**0.96 / 1.95 **

2.60 / 6.19

1.47 / 3.16

1.13 / 2.17

Average

1.05 / 2.12

1.57 / 3.61

**0.75 **/ 1.81

1.68 / 3.98

1.02 / 2.17

0.78 **/ 1.54**

a For models that output vehicle trajectories as OBBs \(i.e., VP-LSTM, MA-GAN, and MACA-GAN\), *minADEO/minFDEO * are also calculated and presented as the lower values in each unit. 

b The average *minADE/minFDE * is calculated as a weighted average based on the number of VRU and vehicle trajectories \( *NumVRU * and *NumVehicle* respectively\) in the test dataset. *minADEavg *= \( *NumVRU *× *minADEVRU *\+ *NumVehicle *× *minADEVehicle*\) */*\( *NumVRU *\+ *NumVehicle*\). 

11 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

In summary, the proposed MACA-GAN model achieves more satisfactory results on the *InD * dataset, particularly excelling in multi-agent trajectory prediction within mixed traffic scenarios. Some illustrative examples are presented in Fig. 6. 

Fig. 6 illustrates the prediction results of our proposed models at four intersections in the *InD * dataset. Additionally, the prediction results of the TUTR model, which performed well in Table 1, and the VP-LSTM model, which also focuses on vehicle–pedestrian trajectory prediction, are shown in Fig. 6 for comparison. These comparisons highlight three key aspects. Firstly, both VP-LSTM and our proposed models treat vehicles as oriented bounding boxes \(OBBs\), resulting in continuous rectangular box outputs for vehicle trajectories. In contrast, TUTR generates continuous trajectory points for both VRUs and vehicles. Secondly, among the baseline models, the transformer-based model, TUTR, has demonstrated favorable performance in VRUs trajectory prediction. However, its accuracy notably diminishes, especially when dealing with turning vehicles and those engaged in intricate interactions. For instance, in the example at the *Frankenburg * intersection, TUTR fails to accurately predict the trajectories of yielding vehicles and turning VRUs. 

This limitation is particularly critical in real-world applications where precise predictions are necessary for safety and efficiency. 

Thirdly, compared with MA-GAN, MACA-GAN, with an additional collision extraction module, achieves better performance for VRUs and vehicles in interactive scenarios. This module enhances the model’s ability to consider and avoid potential collisions among multiple agents, which is essential for navigating complex urban environments. Consequently, MACA-GAN exhibits more stable and superior predictive results across different scenarios, making it a more reliable choice for real-time traffic management and autonomous driving applications. 

Ablation studies are also conducted to test the effectiveness of the collision extraction module. Fig. 7 illustrates the experiments conducted at the *Frankenburg * intersection, which is a challenging, and representative scenario in *InD * dataset. In Fig. 7,  *k * represents the number of times the variety loss is sampled during training. This means that the generator is executed *k * times, and the minimum loss is **Fig. 6. **Predicted trajectories of different models on the *InD * dataset. 

12 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

**Fig. 7. **The *minADE * during training with or without collision extraction module. 

selected and backpropagated. Additionally, *sample * denotes the number of times each trajectory is sampled during performance evaluation. These two parameters are crucial in Social-GAN.\(Gupta et al., 2018\). 

As reported by Gupta et al. \(2018\), training with the variety loss significantly improves accuracy. So, in this study, two sets of experiments are conducted with *k *= 5 *, sample *= 5 and *k *= 20 *, sample *= 20. The values of *minADE * for VRUs and vehicles during training are recorded. The results demonstrate that the collision extraction module could effectively reduce the *minADE * of predicted trajectories when *k *= 20 *, sample *= 20. Increasing both *k * and *sample * significantly decreases the *minADE * and accelerates model convergence. However, it also slows down the training speed due to multiple executions of the generator during training. Therefore, increasing *k * and *sample * can improve the model’s accuracy at the expense of sacrificing some training efficiency. And following the work of \(Gupta et al., 2018\), in this study, *k *= 20 *, sample *= 20 is used in comparison with baseline models. 

*4.5. Interactions among multiple traffic agents*

In this subsection, the study first introduces Distance-Velocity diagram to analyze the yielding behavior of vehicles in the ***VRU- ***

***V**ehicle * interaction process. This diagram helps to visualize how vehicles adjust their speed and distance in response to the presence of VRUs. Next, the trajectory probability distribution of multiple agents is estimated to analyze their collision avoidance behaviors. This step involves assessing how different agents, such as vehicles, bicyclists, and pedestrians, navigate shared spaces to prevent collisions. 

Finally, the risk of collisions is evaluated using traffic conflict techniques, such as Post-Encroachment Time \(PET\). These analyses allow for a comprehensive interpretation of the proposed trajectory prediction model’s capabilities in understanding social interactions and learning from them. 

To achieve this, the *Frankenburg * intersection, which contains a crosswalk, is selected. This intersection is chosen because it captures a diverse range of multi-agent trajectories, including those of vehicles, bicyclists, and pedestrians. The complex interactions observed at the zebra crossing provide a highly representative scenario for analyzing these interactions and evaluating the effectiveness of our model. Therefore, the *Frankenburg * intersection’s dynamic environment, with frequent yielding and collision avoidance maneuvers, serves as an ideal testbed for assessing the model’s performance in real-world conditions. 

*4.5.1. Vehicle yielding behavior analysis*

Generally, a robust trajectory prediction model should be able to accurately predict trajectories of traffic agents in different ***VRU***- 

***V**ehicle * interaction scenarios \(e.g., when vehicles yield or don’t yield\), which could be partially reflected through changes in vehicle velocity. DV diagram was first proposed by Fu et al. \(2018\) to evaluate pedestrian safety at non-signalized crosswalk locations, which works well in describing ***VRU***- ***V**ehicle * interactions. Specifically, the DV diagram assumes that after a vehicle notices a pedestrian crossing at a crosswalk, it goes through two stages: the reaction stage and the braking stage. During the reaction stage, the vehicle maintains a constant velocity, while during the braking stage, it brakes at the maximum deceleration rate determined by the friction coefficient between the wheels and the road surface. Therefore, considering different driver reaction times, the shortest distance required for a vehicle to come to a complete stop before a crosswalk can be expressed as follows: *D*

*v* 2

*min *= *vtr *\+ 2 *g*

\(28\) 

\( *μmax *− *θ*\)

where *v * is the initial velocity of the vehicle at the occurrence of the pedestrian, *tr * is the perception-reaction time of the driver, *g * is the acceleration of gravity, *μmax * is the maximum friction coefficient of the road surface, and *θ * is the angle of roadway slope. 

In this study, the driver reaction time during a ***VRU***- ***V**ehicle * interaction \(the entire reaction period prior to the actual braking\) at 13 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

crosswalks is taken between 0.5 s and 2 s \(Fu et al., 2018\),  *μmax * is set as 0.75 \(Knowles Flanagan et al., 2021\),  *θ * is set as 0, *g * is taken as 10 *m/s* 2. Based on these parameters, *Dmin * can be calculated, which is in a range of \[ *D* 0 *, D* 1\]. Then the DV diagram can be constructed by plotting the vehicle velocity on the horizontal axis and the distance to the crosswalk on the vertical axis. However, different from the work of Fu et al. \(2019\), we present the VD diagram to illustrate velocity changes over distance, with consideration given to the acceleration period following the vehicle’s yielding behavior \(i.e., when the vehicle accelerates off the crosswalk\) to capture the entire interaction process, as depicted in Fig. 8. 

Based on the varying driver reaction times, the vehicle yielding behavior can be further divided into three phases: Phase 1 represents scenarios where the vehicle is unable to stop before the crosswalk due to insufficient reaction time. Phase 2 occurs when the vehicle’s ability to stop before the crosswalk depends on the driver’s reaction time. Phase 3 arises when the vehicle is fully capable of stopping before the crosswalk. Table 2 shows the model’s accuracy in predicting trajectories of VRUs and vehicles across different phases. While TUTR performs better in VRUs trajectory prediction, MACA-GAN excels in vehicle trajectory prediction for both phase 1 

and phase 3, achieving optimal *minADE * and *minFDE*. Particularly for phase 3, which constitutes 85.7 % of the test dataset, MACA-GAN 

demonstrates superior performance across all metrics. And MA-GAN outperforms only in the *minFDE * for VRUs in phase 2 and phase 3, with overall performance slightly inferior to MACA-GAN. It is noteworthy that the trajectories related to ***VRU***- ***V**ehicle * interactions are typically characterized by rapid speed changes, turns, and other challenging maneuvers, which may pose a greater challenge for prediction. 

Although in some areas, vehicles are required to yield to VRUs at the crosswalk, the decision of whether a vehicle stops to yield is also influenced by various complex factors \(e.g., driver behavior, traffic density, and environment\) \(Li et al., 2023a\). Consequently, scenarios where vehicles fail to yield or even violate the rules by accelerating through the crosswalk may also occur. Fig. 9 illustrates four typical ***VRU***- ***V**ehicle * interaction scenarios: \(a\) Stop yielding, \(b\) Slow down yielding, \(c\) Non-yielding Violation, and \(d\) Non-infraction Non-yielding \(i.e., the driver lacks sufficient reaction time to yield, resulting in stopping after passing the crosswalk\). 

Due to TUTR’s inability to output vehicle trajectories in the form of OBBs, the velocity changes calculated based on the vehicle’s central point may not be precise enough, leading to the fluctuation shown in Fig. 9 \(a\). In contrast, Fig. 9 \(a, b\) demonstrates that MACA-GAN is more adept at accurately capturing different yielding behaviors of vehicles, and reflecting the velocity changes of vehicles as they pass through the crosswalk. In the cases of vehicles failing to yield as shown in Fig. 9 \(c, d\), where the velocity changes exhibit strong regularity, models like TUTR and VP-LSTM can also make fairly accurate predictions. Overall, MACA-GAN outperforms MA-GAN in accurately predicting trajectories across various ***VRU***- ***V**ehicle * interaction scenarios and in faithfully reconstructing vehicle velocity changes. This demonstrates the importance of considering collision avoidance and highlights the effectiveness of the collision extraction module. 

*4.5.2. Collision avoidance behavior analysis*

The proposed model can generate multiple trajectories by sampling random noise *z * for *sample * times, enabling the estimation of the probability distributions for predicted trajectories. In line with previous studies \(Bi et al., 2019; Yao et al., 2021\), kernel density estimation is applied to the coordinates of VRUs’ and the central coordinates of vehicles \(i.e., OBBs\) to derive their trajectory distributions. 

The trajectory distributions across different models for ***VRU***- ***VRU **and **V**ehicle*- ***V**ehicle * are presented in Fig. 10. For VRUs, they actively maintain a certain distance from each other to avoid potential collisions and ensure their own safety. For vehicles, behaviors **Fig. 8. **Distance-Velocity diagram for vehicles. 

14 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

**Table 2 **

The ***minADE *** and ***minFDE *** for trajectories related to ***VRU*****- *V****ehicle * interactions. 

Phase

Percentage

Model

VRUs

Vehicles

*minADE / minFDE*

*minADE / minFDE*

Phase1

3.6 %

VP-LSTM

2.21 / 4.64

3.05 / 6.51

TUTR

**0.65 / 1.47**

0.79 / 1.80

MA-GAN

0.96 / 1.51

0.95 / 1.90

MACA-GAN

0.71 / 1.49

**0.77 / 1.71**

Phase2

10.7 %

VP-LSTM

2.08 / 4.63

3.89 / 8.81

TUTR

**0.65 **/ 1.51

**0.82 **/ 1.89

MA-GAN

0.78 / **1.20**

0.99 / 2.12

MACA-GAN

0.70 / 1.46

0.84 / **1.82**

Phase3

85.7 %

VP-LSTM

1.93 / 4.26

3.14 / 7.33

TUTR

**0.70 **/ 1.58

0.89 / 2.06

MA-GAN

0.81 / **1.39**

0.85 / 1.76

MACA-GAN

**0.70 / **1.49

**0.76 / 1.62**

**Fig. 9. **Illustration of the results for ***VRU***- ***V**ehicle * interaction. 

15 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

**Fig. 10. **Collision avoidance behaviors for ***VRU*****- *VRU and V****ehicle*- ***V**ehicle*. The dashed line with an arrow is the true trajectory and the color density is the predicted trajectory distribution. 

such as slowing down to avoid rear-end collisions are also observed. In such scenarios, compared to other models, trajectories generated by MACA-GAN are almost centered around the ground truth. Besides, the predicted distributions of MACA-GAN demonstrate more reasonable interactions, highlighting the model’s effectiveness in capturing the collision avoidance behaviors of multiple agents. 

In a more complex scenario, as depicted in Fig. 11, the scenario involves three pedestrians \( *P* 1 *,P* 2 *,P* 3\), one bicycle \( *P* 4\), and five vehicles \( *V* 1 *,V* 2 *,V* 3 *,V* 4 *,V* 5\). Pedestrian *P* 2 attempts to cross the crosswalk after vehicle *V* 4 has passed. However, considering the potential risk of collisions posed by vehicle *V* 5, the predicted trajectory distribution of *P* 2 clearly indicates a tendency to avoid *V* 4. Vehicle *V* 5, however, either due to a lack of awareness of the pedestrian or driven by an aggressive driver, does not exhibit any deceleration or yielding behavior. Conversely, vehicles *V* 1 *, V* 2 *, V* 3 and *V* 4 choose to either come to a stop or slow down to yield, which effectively helps to avoid a collision with *P* 4 \(a bicycle\). The predicted trajectory distribution of MACA-GAN effectively captures these behaviors. 

*4.5.3. Traffic conflicts analysis*

This study aims to evaluate the risk of collisions between VRUs and vehicles at unsignalized intersections based on traffic conflict techniques, which also serves as a standard to assess the social understanding of different models. 

The concept of Post-Encroachment Time \(PET\) is introduced to assess the risk of conflicts between VRUs and vehicles. PET 

measures the time difference between a road user leaving the conflict point and another road user reaching the same conflict point. It is defined as follows: 

*PET *= *t* 1 − *t* 2

\(29\) 

Where *t* 1 and *t* 2 denote the earlier or later time to reach the conflict point. 

In this study, the conflict points of VRUs and vehicles are first calculated based on their trajectories. Then, the *minADE * of these conflict points are calculated to evaluate the prediction accuracy of different trajectory prediction models. It is important to note that if VRUs or vehicles have already passed the conflict point during the observation stage, they are not included in the calculation. Only the 16 





*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

**Fig. 11. **Collision avoidance behaviors in a more complicated scenario. The dashed line with an arrow is the true trajectory and the color density is the predicted trajectory distribution. 

**Fig. 12. **Comparison between predicted PET and observed PET. 

trajectories and conflict points that occur during the prediction stage are considered. 

As shown in Fig. 12 and Fig. 13, both MACA-GAN and MA-GAN demonstrate accurate predictions of the PET distribution. However, TUTR and VP-LSTM exhibit relatively poor performance. The quantitative results of different models on the count of dangerous interactions, *minADE * for conflict points, and PET error are listed in Table 3. Based on varying levels of interaction between VRUs and vehicles at intersections, PET ≤ 3 s and PET *> * 3 s are used to represent ’dangerous’ and ’non-dangerous’ interaction scenarios \(Navarro 

et al., 2022; Zangenehpour et al., 2016\). The Confusion Matrix is then presented and used to calculate the accuracy of different models in identifying dangerous scenarios based on predicted trajectories. The results show that MACA-GAN correctly identified 392 

dangerous scenarios and 3,613 non-dangerous scenarios, achieving an accuracy of 98.1 %. In contrast, models like TUTR and VP-LSTM 

have relatively lower accuracy. Additionally, MACA-GAN achieves the best results in terms of the *minADE * for conflict points and the error in PET estimation. These results indicate that MACA-GAN is also highly effective in predicting the trajectories of agents involved in dangerous interactions, which is of great significance for improving traffic safety at unsignalized urban intersections. 

**5. Conclusion**

Accurate trajectory prediction is the premise of proactive safety warnings at unsignalized intersections. In this study, an improved generative adversarial network \(GAN\) is proposed to forecast future trajectories of multiple agents at unsignalized intersections. 

17 



*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

**Fig. 13. **Boxplots of PET values. 

**Table 3 **

Count of dangerous interactions, ***minADE*****, **and PET Error for different models. 

Item

Scenarios

Models

VP-LSTM

TUTR

MA-GAN

MACA-GAN

Count of dangerous interactions

TP a

FN

291

148

378

61

348

91

392

47

FP

TN

222

3423

28

3617

54

3591

32

3613

Accuracy b

0.909

0.978

0.964

**0.981**

PET Error

TP \+ FN

1.02

0.90

0.52

**0.48**

FP \+ TN

1.35

1.00

0.66

**0.54**

ALL

1.25

0.97

0.62

**0.52**

***minADE *** for conflict points

TP \+ FN

2.32

2.01

2.11

**1.76**

FP \+ TN

1.74

1.23

1.12

**0.97**

ALL

1.92

1.47

1.40

**1.19**

a Confusion matrix showing the accuracy of the method to identify dangerous scenarios based on predicted trajecties, with the number of positives *P*, negatives *N*, true positives *TP*, true negatives *TN*, false positives *FP*, and false negatives *FN*. 

b Accuracy = \( *TP *\+ *TN*\) */*\( *P *\+ *N*\). 

Attention pooling modules are employed to capture ***VRU***- ***VRU***, ***V**ehicle*- ***V**ehicle*, and ***VRU***- ***V**ehicle * interactions. Moreover, a GCN-based collision extraction module that focuses on collision avoidance behaviors of multiple agents is introduced. Experiments show that the proposed model successfully improves the accuracy of prediction. 

This approach is particularly effective in accurately predicting vehicle trajectories using the oriented bounding box \(OBB\) representation, which provides more precise parameters for conflict risk assessment and warning. For instance, the negligence of vehicles’ 

geometric dimensions may introduce bias in the calculation of conflict points and Post-Encroachment Time \(PET\), resulting in false warnings. Hence, the OBB representation for vehicle trajectories helps the proposed model to achieve better performance. 

Furthermore, different pooling modules contribute to distinguishing heterogeneous kinetic characteristics and complex interactions among multiple agents, enhancing the model’s robustness. Another crucial focus of this study lies in modeling the collision avoidance behaviors of multiple agents. A graph structure, measured by a two-dimensional surrogate safety indicator, characterizes the connections among multiple agents. Graph convolution operations are further introduced to extract and analyze these relationships. The results of ablation experiments demonstrate that this module effectively enhances the accuracy of the model. 

More importantly, the analysis of various yielding behaviors of vehicles, based on the Distance-Velocity diagram and predicted trajectories, reveals the proposed model’s effectiveness in modeling complex interactions among multiple agents, especially their collision avoidance behaviors. This also shows the model’s robustness in handling different interactive scenarios, such as when vehicles yield or don’t yield. Notably, the conflict points, count of dangerous interactions, and Post-Encroachment Time, as computed from these predicted trajectories, also align well with the ground truth. 

This study also has some limitations. While unsignalized intersections lack essential safety measures, some regions enforce traffic regulations that mandate vehicles to yield to VRUs. However, this study did not delve deeply into this aspect. Understanding how traffic regulations constrain multi-agent behavior is a key area for future research. Additionally, future studies could enhance dataset diversity by incorporating data from various regions to enable a more comprehensive evaluation of intersection scenarios and improve model robustness. In terms of trajectory prediction models, Graph Convolutional Network \(GCN\)-based models and Transformer-based models may be promising in multi-agent trajectory prediction. But thorough investigations are needed to effectively integrate behavioral differences and interactions among multiple agents into such models. Furthermore, ensuring the interpretability of socially 18 

*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

aware models, particularly deep learning models, and enhancing their understanding of interactions among multiple agents are crucial for strengthening the models’ robustness. 

**CRediT authorship contribution statement**

**Lei Zhao: **Writing – original draft, Software, Methodology, Conceptualization. **Wei Zhou: **Investigation, Data curation. **Sixuan Xu:** Visualization, Investigation. **Yuzhi Chen: **Validation, Investigation. **Chen Wang: **Supervision, Project administration, Funding acquisition. 

**Declaration of competing interest**

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper. 

**Acknowledgement**

This work was supported in part by the National Key Research and Development Program of China \[grant number: 2023YFE0106800\], the Excellent Youth Foundation of Jiangsu Scientific Committee \[grant number: BK20231531\] and the Post-graduate Research & Practice Innovation Program of Jiangsu Province \[grant number: SJCX24\_0100\]. 

**References**

Alahi, A., Goel, K., Ramanathan, V., Robicquet, A., Fei-Fei, L., Savarese, S., 2016. Social lstm: Human trajectory prediction in crowded spaces, in: *Proceedings of the* *IEEE conference on computer vision and pattern recognition*, pp. 961-971. 

Amirloo, E., Rasouli, A., Lakner, P., Rohani, M., Luo, J., 2022. LatentFormer: Multi-Agent Transformer-Based Interaction Modeling and Trajectory Prediction. *arXiv* *preprint arXiv:2203.01880*. 

Bertugli, A., Calderara, S., Coscia, P., Ballan, L., Cucchiara, R., 2021. AC-VRNN: Attentive Conditional-VRNN for multi-future trajectory prediction. Computer Vision 

and Image Understanding 210. 

Bi, H., Fang, Z., Mao, T., Wang, Z., Deng, Z., Ieee, 2019. Joint Prediction for Kinematic Trajectories in Vehicle-Pedestrian-Mixed Scenes, in: *IEEE/CVF International* *Conference on Computer Vision \(ICCV\)*, Seoul, SOUTH KOREA, pp. 10382-10391. 

Bock, J., Krajewski, R., Moers, T., Runde, S., Vater, L., Eckstein, L., 2020. The inD Dataset: A Drone Dataset of Naturalistic Road User Trajectories at German Intersections, in: *2020 IEEE Intelligent Vehicles Symposium \(IV\)*, pp. 1929-1934. 

Cao, N., Wei, W., Qu, Z., Zhao, L., Bai, Q., 2017. Simulation of pedestrian crossing behaviors at unmarked roadways based on social force model. Discrete Dyn. Nat. 

Soc. 2017, 1–15. 

Chen, A.Y., Chiu, Y.L., Hsieh, M.H., Lin, P.W., Angah, O., 2020. Conflict analytics through the vehicle safety space in mixed traffic flows using UAV image sequences. 

Transp. Res. Part C Emerg. Technol. 119, 102744. 

Chen, P., Zeng, W., Yu, G.Z., Wang, Y.P., 2017. Surrogate Safety Analysis of Pedestrian-Vehicle Conflict at Intersections Using Unmanned Aerial Vehicle Videos. 

*J. Adv. Transp. *

Chen, J.X., Chen, G., Li, Z.J., Wu, Y., Knoll, A., Ieee, 2021. Attention Based Graph Convolutional Networks for Trajectory Prediction, in: *6th IEEE International* *Conference on Advanced Robotics and Mechatronics \(ICARM\)*, Chongqing, PEOPLES R CHINA, pp. 852-857. 

Cheng, H., Sester, M., 2018. Modeling mixed traffic in shared space using LSTM with probability density mapping, in: *2018 21st International Conference on Intelligent* *Transportation Systems \(ITSC\)*. IEEE, pp. 3898-3904. 

Deo, N., Trivedi, M.M., 2018. Convolutional social pooling for vehicle trajectory prediction, in: *Proceedings of the IEEE conference on computer vision and pattern* *recognition workshops*, pp. 1468-1476. 

Ezzati Amini, R., Yang, K., Antoniou, C., 2022. Development of a conflict risk evaluation model to assess pedestrian safety in interaction with vehicles. Accid. Anal. 

Prev. 175, 106773. 

Fang, F., Zhang, P.P., Zhou, B., Qian, K., Gan, Y.H., 2022. Atten-GAN: pedestrian trajectory prediction with GAN based on attention mechanism. Cognitive Comput. 

Feng, J., Wang, C.Y., Xu, C., Kuang, D.M., Zhao, W.Z., 2022. Active collision avoidance strategy considering motion uncertainty of the pedestrian. IEEE Trans. Intell. 

Transp. Syst. 23 \(4\), 3543–3555. 

Firl, J., Stübing, H., Huss, S.A., Stiller, C., 2012. Predictive maneuver evaluation for enhancement of car-to-x mobility data, in: *2012 IEEE Intelligent Vehicles* *Symposium*. IEEE, pp. 558-564. 

Fu, T., Miranda-Moreno, L., Saunier, N., 2018. A novel framework to evaluate pedestrian safety at non-signalized locations. Accid. Anal. Prev. 111, 23–33. 

Fu, T., Hu, W.C., Miranda-Moreno, L., Saunier, N., 2019. Investigating secondary pedestrian-vehicle interactions at non-signalized intersections using vision-based 

trajectory data. Transp. Res. Part C Emerg. Technol. 105, 222–240. 

Geng, M., Cai, Z., Zhu, Y., Chen, X., Lee, D.H., 2023a. Multimodal vehicular trajectory prediction with inverse reinforcement learning and risk aversion at urban 

unsignalized intersections. IEEE Trans. Intell. Transp. Syst. 1–14. 

Geng, M., Chen, Y., Xia, Y., Chen, X., 2023b. Dynamic-learning spatial-temporal Transformer network for vehicular trajectory prediction at urban intersections. 

Transp. Res. Part C Emerging Technol. 156, 104330. 

Govinda, L., Raju, M., Shankar, K., 2022. Pedestrian-vehicle interaction severity level assessment at uncontrolled intersections using machine learning algorithms. *Saf. *

*Sci. * 153. 

Gupta, A., Johnson, J., Fei-Fei, L., Savarese, S., Alahi, A., 2018. Social gan: Socially acceptable trajectories with generative adversarial networks, in: *Proceedings of the* *IEEE conference on computer vision and pattern recognition*, pp. 2255-2264. 

Helbing, D., Molnar, P., 1995. Social force model for pedestrian dynamics. Phys. Rev. E 51 \(5\), 4282. 

Høye, A., Laureshyn, A., 2019. SeeMe at the crosswalk: Before-after study of a pedestrian crosswalk warning system. Transp. Res. Part F Psychol. Behav. 60, 723–733. 

Huang, Y., Bi, H., Li, Z., Mao, T., Wang, Z., 2019. Stgat: Modeling spatial-temporal interactions for human trajectory prediction, in: *Proceedings of the IEEE/CVF *

*international conference on computer vision*, pp. 6272-6281. 

Huang, Z., Wang, J., Pi, L., Song, X., Yang, L., 2021. LSTM based trajectory prediction model for cyclist utilizing multiple interactions with environment. Pattern 

Recognition 112, 107800. 

Ju, C., Wang, Z., Long, C., Zhang, X., Chang, D.E., 2020. Interaction-aware kalman neural networks for trajectory prediction, in: *2020 IEEE Intelligent Vehicles* *Symposium \(IV\)*. IEEE, pp. 1793-1800. 

Kalatian, A., Farooq, B., 2022. A context-aware pedestrian trajectory prediction framework for automated vehicles. Transp. Res. Part C Emerg. Technol. 134, 103453. 

Keller, C.G., Hermes, C., Gavrila, D.M., 2011. Will the pedestrian cross? probabilistic path prediction based on learned motion features, in: *Pattern Recognition: 33rd* *DAGM Symposium, Frankfurt/Main, Germany, August 31*– *September 2, 2011. Proceedings 33*. Springer, pp. 386-395. 

19 

*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

Knowles Flanagan, S., Tang, Z., He, J., Yusoff, I., 2021. Investigating and modeling of cooperative vehicle-to-vehicle safety stopping distance. Future Internet 13 \(3\), 

68. 

Kosaraju, V., Sadeghian, A., Martín-Martín, R., Reid, I., Savarese, S., 2019. Social-BiGAT: Multimodal Trajectory Forecasting using Bicycle-GAN and Graph Attention Networks. *Advances in neural information processing systems * 32. 

Lan, Z., Jiang, Y., Mu, Y., Chen, C., Li, S.E., 2023. SEPT: Towards Efficient Scene Representation Learning for Motion Prediction, in: *The Twelfth International* *Conference on Learning Representations*. 

Lanzaro, G., Sayed, T., Alsaleh, R., 2022. Can motorcyclist behavior in traffic conflicts be modeled? a deep reinforcement learning approach for motorcycle-pedestrian 

interactions. Transportmetrica B 10 \(1\), 396–420. 

Li, R., Katsigiannis, S., Shum, H.P.H., 2022b. Multiclass-SGCN: Sparse Graph-Based Trajectory Prediction with Agent Class Embedding, in: *2022 IEEE International* *Conference on Image Processing \(ICIP\)*, pp. 2346-2350. 

Li, H., Hu, H., Zhang, Z., Zhang, Y., 2023a. The role of yielding cameras in pedestrian-vehicle interactions at un-signalized crosswalks: an application of game 

theoretical model. Transp. Res. Part F Psychol. Behav. 92, 27–43. 

Li, J., Ma, H., Zhang, Z., Li, J., Tomizuka, M., 2022a. Spatio-temporal graph dual-attention network for multi-agent prediction and tracking. IEEE Trans. Intell. Transp. 

Syst. 23 \(8\), 10556–10569. 

Li, J., Ni, Y., Sun, J., 2023b. A two-layer integrated model for cyclist trajectory prediction considering multiple interactions with the environment. Transp. Res. Part C 

Emerg. Technol. 155, 104304. 

Liu, Y., Qi, X., Sisbot, E.A., Oguchi, K., 2022b. Multi-Agent Trajectory Prediction with Graph Attention Isomorphism Neural Network, in: *2022 IEEE Intelligent Vehicles* *Symposium \(IV\)*, pp. 273-279. 

Liu, S.H., Liu, H.B., Bi, H.K., Mao, T.L., 2020. CoL-GAN: plausible and collision-less trajectory prediction by attention-based GAN. IEEE Access 8, 101662–101671. 

Liu, X., Wang, Y., Jiang, K., Zhou, Z., Nam, K., Yin, C., 2022a. Interactive trajectory prediction using a driving risk map-integrated deep learning method for 

surrounding vehicles on highways. IEEE Trans. Intell. Transp. Syst. 23 \(10\), 19076–19087. 

Malviya, V., Kala, R., 2022. Trajectory prediction and tracking using a multi-behaviour social particle filter. Appl. Intell. 52 \(7\), 7158–7200. 

Mo, X., Huang, Z., Xing, Y., Lv, C., 2022. Multi-agent trajectory prediction with heterogeneous edge-enhanced graph attention network. IEEE Trans. Intell. Transp. 

Syst. 23 \(7\), 9554–9567. 

Nasernejad, P., Sayed, T., Alsaleh, R., 2021. Modeling pedestrian behavior in pedestrian-vehicle near misses: a continuous Gaussian Process Inverse Reinforcement 

Learning \(GP-IRL\) approach. Accid. Anal. Prev. 161, 106355. 

Navarro, B., Miranda-Moreno, L., Saunier, N., Labbe, A., Fu, T., 2022. Do stop-signs improve the safety for all road users? a before-after study of stop-controlled 

intersections using video-based trajectories and surrogate measures of safety. Accid. Anal. Prev. 167, 106563. 

Nayak, A., Eskandarian, A., Doerzaph, Z., 2022. Uncertainty estimation of pedestrian future trajectory using Bayesian approximation. IEEE Open J. Intell. Transp. 

Syst. 3, 617–630. 

Noh, B., Yeo, H., 2022. A novel method of predictive collision risk area estimation for proactive pedestrian accident prevention system in urban surveillance 

infrastructure. Transp. Res. Part C Emerg. Technol. 137, 103570. 

Pang, S.M., Cao, J.X., Jian, M.Y., Lai, J., Yan, Z.Y., 2022. BR-GAN: a pedestrian trajectory prediction model combined with behavior recognition. IEEE Trans. Intell. 

Transp. Syst. 24609–24620. 

Rudenko, A., Palmieri, L., Arras, K.O., 2018. Joint long-term prediction of human motion using a planning-based social force approach, in: *2018 IEEE International* *Conference on Robotics and Automation \(ICRA\)*. IEEE, pp. 4571-4577. 

Saadatnejad, S., Bahari, M., Khorsandi, P., Saneian, M., Moosavi-Dezfooli, S.-M., Alahi, A., 2022. Are socially-aware trajectory prediction models really socially- 

aware? Transp. Res. Part C Emerging Technol. 141, 103705. 

Sadeghian, A., Kosaraju, V., Sadeghian, A., Hirose, N., Rezatofighi, H., Savarese, S., 2019. SoPhie: An Attentive GAN for Predicting Paths Compliant to Social and Physical Constraints, in: *2019 IEEE/CVF Conference on Computer Vision and Pattern Recognition \(CVPR\)*, pp. 1349-1358. 

Salzmann, T., Ivanovic, B., Chakravarty, P., Pavone, M., 2020. Trajectron\+\+: Dynamically-feasible trajectory forecasting with heterogeneous data, in: *Computer* *Vision*– *ECCV 2020: 16th European Conference, Glasgow, UK, August 23*– *28, 2020, Proceedings, Part XVIII 16*. Springer, pp. 683-700. 

Schneider, N., Gavrila, D.M., 2013. Pedestrian Path Prediction with Recursive Bayesian Filters: A Comparative Study, in: *Pattern Recognition*. Springer Berlin Heidelberg, Berlin, Heidelberg, pp. 174-183. 

Schubert, R., Richter, E., Wanielik, G., 2008. Comparison and evaluation of advanced motion models for vehicle tracking, in: *2008 11th International Conference on* *Information Fusion*, pp. 1-6. 

Shi, L., Wang, L., Long, C., Zhou, S., Zhou, M., Niu, Z., Hua, G., 2021. SGCN: Sparse graph convolution network for pedestrian trajectory prediction, in: *Proceedings of* *the IEEE/CVF Conference on Computer Vision and Pattern Recognition*, pp. 8994-9003. 

Shi, L., Wang, L., Zhou, S., Hua, G., 2023a. Trajectory Unified Transformer for Pedestrian Trajectory Prediction, in: *Proceedings of the IEEE/CVF International Conference* *on Computer Vision*, pp. 9675-9684. 

Shi, S., Jiang, L., Dai, D., Schiele, B., 2023b. Mtr\+\+: Multi-agent motion prediction with symmetric scene modeling and guided intention querying. *arXiv preprint* *arXiv:2306.17770*. 

Song, X., Chen, K., Li, X., Sun, J.H., Hou, B.C., Cui, Y., Zhang, B.C., Xiong, G., Wang, Z.L., 2021. Pedestrian trajectory prediction based on deep convolutional LSTM 

network. IEEE Trans. Intell. Transp. Syst. 22 \(6\), 3285–3302. 

Venthuruthiyil, S.P., Chunchu, M., 2022. Anticipated Collision Time \(ACT\): a two-dimensional surrogate safety indicator for trajectory-based proactive safety 

assessment. Transp. Res. Part C Emerg. Technol. 139, 103655. 

Wang, C., Xie, Y., Huang, H., Liu, P., 2021. A review of surrogate safety measures and their applications in connected and automated vehicles safety modeling. *Accid. *

*Anal. Prev. * 157. 

Wang, Z., Guo, J., Hu, Z., Zhang, H., Zhang, J., Pu, J., 2023. Lane transformer: a high-efficiency trajectory prediction model. IEEE Open J. Intell. Transp. Syst. 4, 2–13. 

Wang, C., Xu, C., Dai, Y., 2019. A crash prediction method based on bivariate extreme value theory and video-based vehicle trajectory data. Accid. Anal. Prev. 123, 

365–373. 

Xie, X., Zhang, C., Zhu, Y., Wu, Y.N., Zhu, S.-C., 2021. Congestion-aware multi-agent trajectory prediction for collision avoidance, in: *2021 IEEE International* *Conference on Robotics and Automation \(ICRA\)*. IEEE, pp. 13693-13700. 

Xie, G., Gao, H., Qian, L., Huang, B., Li, K., Wang, J., 2018. Vehicle trajectory prediction by integrating physics- and maneuver-based approaches using interactive 

multiple models. IEEE Trans. Ind. Electron. 65 \(7\), 5999–6008. 

Yan, S., Xiong, Y., Lin, D., 2018. Spatial temporal graph convolutional networks for skeleton-based action recognition, in: *Proceedings of the AAAI conference on* *artificial intelligence*. 

Yang, S., Wang, W., Jiang, Y., Wu, J., Zhang, S., Deng, W., 2019. What contributes to driving behavior prediction at unsignalized intersections? Transp. Res. Part C 

Emerg. Technol. 108, 100–114. 

Yao, R., Zeng, W., Chen, Y., He, Z., 2021. A deep learning framework for modelling left-turning vehicle behaviour considering diagonal-crossing motorcycle conflicts 

at mixed-flow intersections. Transp. Res. Part C Emerg. Technol. 132, 103415. 

Yu, C., Ma, X., Ren, J., Zhao, H., Yi, S., 2020. Spatio-temporal graph transformer networks for pedestrian trajectory prediction, in: *Computer Vision*– *ECCV 2020: 16th* *European Conference, Glasgow, UK, August 23*– *28, 2020, Proceedings, Part XII 16*. Springer, pp. 507-523. 

Zangenehpour, S., Strauss, J., Miranda-Moreno, L.F., Saunier, N., 2016. Are signalized intersections with cycle tracks safer? a case–control study based on automated 

surrogate safety analysis using video data. Accid. Anal. Prev. 86, 161–172. 

Zhang, S.L., Abdel-Aty, M., Wu, Y.N., Zheng, O., 2020. Modeling pedestrians’ near-accident events at signalized intersections using gated recurrent unit \(GRU\). Accid. 

Anal. Prev. 148, 105844. 

Zhang, S.L., Abdel-Aty, M., 2022. Real-time pedestrian conflict prediction model at the signal cycle level using machine learning models. IEEE Open J. Intell. Transp. 

Syst. 3, 176–186. 

20 

*L. Zhao et al. *

*Transportation* *Research* *Part* *C* *171* *\(2025\)* *104974* 

Zhang, C., Berger, C., 2023. Pedestrian Behavior Prediction Using Deep Learning Methods for Urban Scenarios: A Review. *IEEE Trans. Intell. Transp. Syst. *

Zhang, X., Chen, H., Yang, W.Y., Jin, W.Q., Zhu, W.W., 2021. Pedestrian path prediction for autonomous driving at un-signalized crosswalk using W/CDM and MSFM. 

IEEE Trans. Intell. Transp. Syst. 22 \(5\), 3025–3037. 

Zhang, P., Ouyang, W.L., Zhang, P.F., Xue, J.R., Zheng, N.N., Soc, I.C., 2019. SR-LSTM: State Refinement for LSTM towards Pedestrian Trajectory Prediction, in: *32nd* *IEEE/CVF Conference on Computer Vision and Pattern Recognition \(CVPR\)*. Ieee, Long Beach, CA, pp. 12077-12086. 

Zhang, W., Cheng, H., Johora, F.T., Sester, M., 2023b. ForceFormer: exploring social force and transformer for pedestrian trajectory prediction, in: *2023 IEEE *

*Intelligent Vehicles Symposium \(IV\)*. IEEE, pp. 1-7. 

Zhang, K., Li, L., 2022. Explainable multimodal trajectory prediction using attention models. Transp. Res. Part C Emerg. Technol. 143, 103829. 

Zhang, K., Feng, X., Wu, L., He, Z., 2022. Trajectory prediction for autonomous driving using spatial-temporal graph attention transformer. IEEE Trans. Intell. Transp. 

Syst. 1–11. 

Zhang, X., Yan, X., 2023. Predicting collision cases at unsignalized intersections using EEG metrics and driving simulator platform. Accid. Anal. Prev. 180, 106910. 

Zhang, E., Zhang, R., Masoud, N., 2023a. Predictive trajectory planning for autonomous vehicles at intersections using reinforcement learning. Transp. Res. Part C 

Emerg. Technol. 149, 104063. 

Zhou, W., Liu, Y., Zhao, L., Xu, S., Wang, C., 2023a. Pedestrian Crossing Intention Prediction From Surveillance Videos for Over-the-Horizon Safety Warning. *IEEE *

*Trans. Intell. Transp. Syst. *

Zhou, W., Wang, C., Ge, Y., Wen, L., Zhan, Y., 2023b. All-Day Vehicle Detection From Surveillance Videos Based on Illumination-Adjustable Generative Adversarial Network. *IEEE Trans. Intell. Transp. Syst. *

Zhou, Z., Peng, Y., Cai, Y., 2020. Vision-based approach for predicting the probability of vehicle–pedestrian collisions at intersections. IET Intel. Transport Syst. 14 

\(11\), 1447–1455. 

21 



# Document Outline

+ Multi-agent trajectory prediction at unsignalized intersections: An improved generative adversarial network accounting for ...   
	+ 1 Introduction 
	+ 2 Literature review  
		+ 2.1 Multi-agent trajectory prediction 
		+ 2.2 Interactions among multiple agents 

	+ 3 Methodology  
		+ 3.1 Problem definition 
		+ 3.2 Overall framework 
		+ 3.3 LSTM-based trajectory encoder 
		+ 3.4 Attention pooling modules for multi-agent interactions  
			+ 3.4.1 VRU-VRU 
			+ 3.4.2 Vehicle-Vehicle 
			+ 3.4.3 VRU-Vehicle 

		+ 3.5 GCN-based collision extraction module  
			+ 3.5.1 Graph representation 
			+ 3.5.2 Spatio-temporal graph convolution 

		+ 3.6 LSTM-based trajectory decoder 
		+ 3.7 Discriminator and losses 

	+ 4 Experiments  
		+ 4.1 Dataset and data pre-processing 
		+ 4.2 Evaluation metrics 
		+ 4.3 Implementation details 
		+ 4.4 Trajectory prediction results  
			+ 4.4.1 Models for comparison 
			+ 4.4.2 Results of predicted trajectories 

		+ 4.5 Interactions among multiple traffic agents  
			+ 4.5.1 Vehicle yielding behavior analysis 
			+ 4.5.2 Collision avoidance behavior analysis 
			+ 4.5.3 Traffic conflicts analysis 


	+ 5 Conclusion 
	+ CRediT authorship contribution statement 
	+ Declaration of competing interest 
	+ Acknowledgement 
	+ References



