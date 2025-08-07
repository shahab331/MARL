Multi-Agent Reinforcement Learning-based Cooperative Autonomous Driving in Smart Intersections

Taoyuan Yu, Kui Wang, Zongdian Li, Tao Yu, and Kei Sakaguchi Abstract— Unsignalized intersections pose significant safety CAVs and smart roadside infrastructure \(e.g., RSUs\), laying a and efficiency challenges due to complex traffic flows. This foundation for constructing cooperative driving systems \[7\]. 

paper proposes a novel roadside unit \(RSU\)-centric cooperative Building upon V2I capabilities, the design of RSU-based driving system leveraging global perception and vehicle-to-cooperative systems has appeared as an attractive research infrastructure \(V2I\) communication. The core of the system is an RSU-based decision-making module using a two-stage topic for both academia and industry in recent years \[8\], hybrid reinforcement learning \(RL\) framework. At first, policies

\[9\]. Research on optimizing traffic flow at intersections has are pre-trained offline using conservative Q-learning \(CQL\) explored various methods. Traditional methods often rely on combined with behavior cloning \(BC\) on collected dataset. 

model-based optimization or game-theoretic frameworks to Subsequently, these policies are fine-tuned in the simulation allocate right-of-way and manage traffic, achieving progress using multi-agent proximal policy optimization \(MAPPO\), aligned with a self-attention mechanism to effectively solve in reducing delays under certain conditions \[10\]–\[12\]. How-inter-agent dependencies. RSUs perform real-time inference ever, these methods typically lack the adaptability required to based on the trained models to realize vehicle control via V2I effectively handle the high complexity and uncertainty inher-communications. Extensive experiments in CARLA environ-ent in dynamic real-world traffic scenarios. To address these ment demonstrate high effectiveness of the proposed system, limitations, multi-agent reinforcement learning \(MARL\) has by: \(i\) achieving failure rates below 0.03% in coordinating three connected and autonomous vehicles \(CAVs\) through emerged as a promising alternative, with research investigat-complex intersection scenarios, significantly outperforming the ing hierarchical structures or integrating perception modules traditional Autoware control method, and \(ii\) exhibiting strong to enhance coordination \[13\]–\[15\]. Nevertheless, many ex-robustness across varying numbers of controlled agents and isting MARL applications in this domain tend to treat all shows promising generalization capabilities on other maps. 

vehicles uniformly, often overlooking the critical need for distinct policies tailored to specific driving roles \(e.g., turning I. INTRODUCTION

left, going straight, turning right\) and failing to fully capture Intersection management is regarded as a bottleneck in the complex interaction dynamics. 

the development of intelligent transportation systems \(ITS\), Further advancements aim to enhance MARL’s capabilities considering the complex and uncertain nature of urban in complex environments. Self-attention mechanisms have intersections \[1\]. According to statistics from the Federal been incorporated to dynamically model inter-agent depen-Highway Administration \(FHWA\) and the National High-dencies, potentially improving generalization and decision way Traffic Safety Administration \(NHTSA\), intersection-efficiency \[16\], \[17\]. However, the effectiveness validation related fatalities account for a substantial proportion of total of adopting self-attention in MARL is still unexplored, traffic accident deaths, especially at unsignalized intersec-particularly its adaptability to dynamically varying num-tions, which reportedly accounted for 68% of such fatalities bers of interacting vehicles within realistic transportation in 2024 \[2\], \[3\]. Unsignalized intersections have become contexts like unsignalized intersections. Similarly, hybrid accident hotspots due to blind spots and the lack of clear offline-online RL frameworks offer potential benefits by arXiv:2505.04231v1 \[cs.RO\] 7 May 2025

interaction rules between motor vehicles, non-motorized leveraging real-world data for safer and more efficient policy vehicles, and pedestrians. In such environments, connected learning \[18\]–\[21\]. However, the practical implementation and autonomous vehicles \(CAVs\) should possess highly and demonstrated effectiveness of these hybrid approaches in effective perception, prediction, and coordinated decision-coordinating multiple cooperative vehicles through complex making capabilities to minimize conflicts and ensure safe and real-world intersection scenarios still require deeper and smooth driving \[4\]. 

investigation. Therefore, there exists a research gap in devel-With the popularization of autonomous vehicles \(AVs\), oping and validating an integrated MARL framework capable mixed traffic scenarios involving AVs and human-driven of robustly and efficiently coordinating vehicles with diverse vehicles \(HDVs\) are becoming common, thereby intro-intentions within the complex dynamics of intersections. 

ducing novel challenges to traffic participants. Vehicle-to-To address such challenges, we propose an innovative everything \(V2X\) communication technologies have emerged RSU-centric intelligent management system for unsignalized as a promising solution to improve roadway efficiency intersections. Utilizing bird-eye-view \(BEV\) perception from and safety \[5\], typically including vehicle-to-vehicle \(V2V\), RSU-mounted LiDAR, the system employs a centralized vehicle-to-infrastructure \(V2I\), vehicle-to-pedestrian \(V2P\), MARL decision module featuring role-specific policy net-and vehicle-to-network \(V2N\) links \[6\]. Among these, V2I works integrated with a self-attention mechanism, allow-communication facilitates real-time data exchange between ing for dynamic modeling of interactions between distinct

Fig. 1: High-level system design of the RSU-CAVs cooperative system driving roles and flexible adaptation to varying numbers or unsafe maneuvers in unsignalized interactions. Instead, of vehicle participants. The policy networks are developed our framework enhances collective safety and overall traffic using a two-stage hybrid learning approach, involving offline throughput by resolving conflicts harmoniously. 

pre-training on the collected dataset, followed by online To effectively manage the intersection’s complexities and fine-tuning in the simulation environment. The proposed uncertainties, the RSU utilizes adaptive decision-making system demonstrates significant advantages in adaptability, policies developed through an RL-based method. This generalization, safety, and efficiency, while also reducing method begins by employing offline RL to instill founda-model deployment complexity and computational demands. 

tional driving knowledge and essential interaction behaviors The key contributions of this research are as follows: into the policy from collected datasets, establishing a robust

• A novel hybrid RL framework combining offline pre-and competent initial strategy. Subsequently, these founda-training and online fine-tuning techniques to enable co-tional policies undergo targeted refinement using online RL

operative driving for CAVs at unsignalized intersections. 

within a simulation environment. This allows the policies

• Development of personalized policy networks tailored to adapt to the intersection’s unique dynamic characteristics to distinct driving roles \(e.g., left-turn, straight, right-and optimize performance for the required multi-vehicle co-turn\) at intersections. 

operative tasks. Compared to learning entirely from scratch, 

• Integration of a self-attention mechanism into role-this hybrid RL approach offers the advantages of accelerating based MARL to enhance policy adaptability to varying learning convergence during the online refinement phase and vehicle numbers and model dynamic interactions. 

ultimately yielding coordination policies that are more robust

• Demonstration of the model’s generalization capability and effective in handling real-world complexities. Further-and rapid adaptability across diverse unsignalized inter-more, deploying the computationally intensive analysis and section scenarios. 

multi-vehicle coordination logic onto the RSU also reduces The remainder of the paper is structured as follows: the processing burden on individual CAVs. This allocation Section II presents the overall architecture of the RSU-of tasks improves the system’s real-time responsiveness and CAVs cooperative system. Section III describes the proposed simplifies requirements for the CAVs \[23\]. 

algorithm in detail. Section IV demonstrates experiment As CAVs approach the intersection, they maintain contin-results. Finally, Section V summarizes the paper and outlines uous information exchange with the RSU. Based on real-future research directions. 

time traffic data and the CAVs’ approach trajectories, the RSU determines each vehicle’s driving role \(e.g., left-turn, II. RSU-CAVS COOPERATIVE SYSTEM

straight, right-turn\). Subsequently, leveraging its pre-loaded The overall system architecture of the proposed RSU-CAV

and role-based strategy networks within the centralized de-cooperative framework is illustrated in Fig. 1. This system cision module, the RSU computes vehicle control signals, employs an RSU, equipped with sensors like LiDAR, for including throttle input, braking force, and steering angles. 

comprehensive intersection monitoring \[22\] and centralized These control commands are transmitted in real-time to the decision-making for multiple CAVs at an unsignalized inter-corresponding CAVs through V2I communication, enabling section. Leveraging the RSU’s BEV perception, this central-direct command execution. Concurrently, the RSU continu-ized method overcomes the inherent limitations of individual ously monitors the comprehensive real-time traffic conditions vehicle perception, providing a global understanding of the at the intersection, including the states and predicted move-traffic situation essential. This contrasts with individualistic ments of CAVs, observed HDVs, and pedestrians, alongside methods, where each vehicle optimizes only its own goals, traffic flow smoothness, collision risks, and any abnormal which can lead to competitive standoffs, inefficient gridlocks, situations. This continuous monitoring provides the neces-

Fig. 2: Offline-online hybrid RL algorithm framework design sary real-time inputs for the RSU’s decision networks and B. Action Space

facilitates ongoing performance evaluation. 

Throughout the learning framework, we define a unified two-dimensional continuous action space A for the vehicle. 

III. HYBRID REINFORCEMENT LEARNING FRAMEWORK

It is structured as:

a\(t\) = \[a

2

\(2\)

As shown in Fig. 2, we propose a two-stage learning acc, asteer\] ∈ R

framework to develop effective cooperative driving strategies where aacc denotes the longitudinal acceleration and asteer for complex unsignalized intersections. This approach first denotes the steering angular velocity. It is important to employs offline pre-training on the collected dataset, using note that during the offline pre-training phase, as ground-offline RL to safely learn foundational driving skills and truth control signals are unavailable in the source data, the traffic priors. Subsequently, online fine-tuning within the action a\(t\) in the dataset is estimated by analyzing the CARLA simulator \[24\] allows agents to adapt to specific state transitions between consecutive changes in velocity and environment dynamics. This synergistic framework combines heading. In the online fine-tuning phase, the policy network the safety and data efficiency of offline learning with the directly outputs two-dimensional action. 

adaptability and performance optimization capabilities of online interaction. The specific methodologies for offline pre-C. Reward Function

training and online fine-tuning are discussed in this section. 

To effectively guide the agent in learning desired cooperative

driving

behaviors

during

complex

online

A. Observation Space

interactions, 

we design

a

structured reward function

Ronline\(s\(t\), a\(t\), s\(t \+ 1\)\) to translate high-level objectives At each time step t, the state space can be defined into real-time feedback. The overall reward r\(t\) is structured s\(t\), which encompasses all traffic participants monitored as:

by RSU within the intersection. the RSU utilizes the global X

r\(t\) =

wkrk\(s\(t\), a\(t\), s\(t \+ 1\)\), 

\(3\)

information to generate specific perspective information for each CAV, constructing an individual observation vector where ri denotes individual reward components and wi de-o\(t\). This construction process, denoted conceptually as notes the corresponding weights. The reward terms include: o\(t\) = O\(s\(t\)\), reflects simulated perception and processing ri ∈ \{rsafety, reff, rcomfort, 

limitations, meaning each o\(t\) is a partially observable and \(4\)

r

potentially noisy representation of the true state s\(t\). The task, ryield, rcoop, rpenalty\}

observation o\(t\) is decomposed as:

where rsafety denotes the penalty for hazardous behavior based on metrics like minimum time-to-collision \(TTC\) and o\(t\) = \[ocore, oveh, oped, orole, octx\], \(1\)

distance to nearby vehicles or pedestrians; reff denotes the efficiency that encourages maintaining a reasonable speed where ocore denotes the ego vehicle features including speed that is compatible with traffic flow; rcomfort denotes the magnitude, global position, heading angle, distance to inter-penalty for large acceleration changes; rtask denotes the section center, and junction occupancy status; oveh denotes reward for all agents to cooperatively reach the navigation relative positions and velocities of nearby vehicles within target; ryield and rcoop denotes the rewards for promoting a predefined ranged; oped denotes information on nearby compliance with traffic rules and cooperation; and rpenalty pedestrians, including detection flags, distance, and relative denotes a severe penalty imposed on events like collisions angle; orole denotes the one-hot encoding of the agent’s or timeouts. Each term is scaled by its corresponding weight role \(e.g., left-turn, straight, or right-turn\); and octx denotes wk, where wsafety and wpenalty are typically assigned larger scenario-level identifiers used to curriculum learning. 

values due to their critical safety implications. 

D. Offline Pre-training: Networks and Algorithm to information from different representation subspaces at The primary goal of the offline pre-training phase is different positions. The core component is the scaled dot-to provide a high-quality initialization for the subsequent product attention:

online fine-tuning stage. In this stage, we train models QK⊤ 

√

independently for each driving role \(left-turn, straight, right-A\(Q, K, V \) = softmax

V

\(7\)

dk

turn\) to incorporate role-specific prior knowledge. We first where Q, K, and V denote the query, key, and value partition the InD dataset \[25\] based on vehicle intentions to matrices, and d

create subsets D

k denotes the dimension of the keys. MHSA role. 

computes h attention ’heads’ in parallel. For each head i, For each subset, we apply an offline reinforcement learn-the input embedding E is linearly projected using learned ing algorithm that combines CQL with BC \[26\] \[27\]. The weights W Q, W K , W V to obtain the head’s specific query, algorithm is implemented using an actor-critic framework i

i

i

key, and value:

to learn effectively from fixed datasets while mitigating distributional shift and imitating expert behavior. 

hi = Attention\(EW Q, EW K , EW V \)

\(8\)

i

i

i

To stabilize learning and reduce Q-value overestimation, The outputs of the parallel heads are then concatenated and the critic uses twin Q-networks Qθ , Q

with target

i,1

θi,2

linearly projected using weights W O to produce the final networks. Each Q-network is trained with the following MHSA output:

objective:



M\(E\) = Concat\(head

1



1, . . . , headh\)W O

\(9\)

LQ\(θi,j\) =E\(o,a,r,o′\)∼D

\(Q

\(o, a\) − y\)2

role=i

θ

2

i,j

\(5\)

Here, E denotes the initial embedded observation features

\+ α

derived from the online observation ot via a learnable linear CQLLCQL\_reg\(θi,j \)

projection layer, and W Q, W K , W V , W O denote trainable i

i

i

Here, y = r \+ γ\(1 − d\) minj Qθ′ \(o′, πϕ \(o′\)\) denotes the i,j

i

weight matrices. 

TD target computed using target Q networks and the current Online learning proceeds via an interact-learn loop. Agents policy. 

generate trajectories:

The policy network πϕ is trained by minimizing the BC

i

loss along with maximizing the expected conservative Q-τ = \{\(ot, at, rt\+1, Vψ\(ot\), log πϕ \(a \(10\)

role

t | ot\)\)\}T

t=0

value:

Advantage estimates and returns are computed using generalized advantage estimation \(GAE\): Lπ\(ϕi\) =Eo∼D

− min Q

\(o, π \(o\)\)

role=i

θi,j

ϕi

j=1,2

\(6\)

T −t−1

ˆ

X

\+ λ



AGAE =

\(γλ\)lδ

BCE\(o,a\)∼D

∥π \(o\) − a∥2

t

t\+l, 

δt = rt\+1 \+γVψ\(ot\+1\)−Vψ\(ot\)

role=i

ϕi

l=0

where αCQL and λBC denotes hyperparameters controlling \(11\)

the strength of CQL regularization and BC imitation, respec-ˆ

Rt = ÂGAE \+ V

t

ψ \(ot\)

\(12\)

tively. 

To enhance data efficiency, we adopt prioritized experience Each role-specific actor πϕ

and critic Q

are pa-

role

θrole

replay \(PER\). Each transition t is assigned a priority p rameterized by multi-layer perceptrons \(MLPs\), which take t

proportional to its absolute TD error |δ

normalized state inputs s

t|, and sampled with

t sampled from Drole. The output

probability P \(t\) ∝ p

corresponds to action distribution parameters or state-action t. To correct the bias introduced by this non-uniform sampling, importance sampling \(IS\) weights are values. 

applied:

Self-attention are not introduced at this stage to focus 1

β

training on extracting robust role-based patterns using stan-wt =

\(13\)

dard MLPs. Training stability is further improved by soft B · P \(t\)

target updates and the adam optimizer. Successful offline Here, B denotes the size of the replay buffer, and β denotes training yields a set of pre-trained weights for the role-an exponent that controls the amount of importance sampling conditioned actor and critic networks, which are reused correction. 

during the online fine-tuning phase to accelerate learning and The shared critic is updated to minimize the weighted enhance performance. 

value loss:

h

i

E. Online Fine-tuning: Networks and Algorithm LV F \(ψ\) = Et∼PER wt\(Vψ\(ot\) − ˆ

Rt\)2

\(14\)

The online fine-tuning phase employs the MAPPO al-where ˆ

Rt denotes the target return calculated in Eq.\(12\). 

gorithm \[28\], selected for its effectiveness in multi-agent Each role-specific actor πϕ

is trained using the following

coordination. This stage builds upon the offline models by role

weighted objective, which includes the PPO clipped surro-integrating role-specific actor networks \(πϕ , π

, π

\)

left

ϕstraight

ϕright

gate loss and an entropy bonus S\[·\]: with a shared critic network Vψ. 

h

To improve reasoning over dynamic environments, we LCLIP\+S\(ϕrole\) = Et∼PER wt − LCLIP\(ϕ

t

role\)

augment both actor and critic networks with multi-head self-

\(15\)

i

attention \(MHSA\). MHSA allows the model to jointly attend

− c2 · S\[πϕ \]\(o

role

t\)

\(a\)

Fig. 4: Offline pre-training results A. Baselines and Evaluation Metrics

We used online-only MAPPO as part of an ablation study; we trained a MAPPO agent that undergoes no offline pre-training and starts training directly in CARLA from scratch \(with the network structure and algorithm parameters being the same as the online phase of our proposed method\), used \(b\)

to compare and evaluate the performance of our proposed Fig. 3: Experimental scenario and generalization scenario algorithm. We will primarily compare them in terms of settings \(a\) CARLA example map, \(b\) Real intersection map convergence speed. Additionally, we employ the open-source autonomous driving software stack, Autoware Universe \[29\]

as a representative of traditional autonomous driving systems. 

The PPO surrogate loss LCLIP

In our experiments, Autoware is configured to control a t

is defined as:

single vehicle navigating the intersection within the identical LCLIP = min r Â

t

t

t, clip\(rt, 1 − ϵ, 1 \+ ϵ\) Ât

\(16\)

scenario used for our single-agent RL tests \(i.e., 1 Autoware-controlled vehicle, 4 background Traffic Manager vehicles, where ϵ denotes the PPO clipping hyperparameter, and rt and 3 pedestrians\). Its performance provides a benchmark denotes the probability ratio between the current policy and for comparison against established methods. 

the old policy:

π

B. Offline Pre-training Results

ϕ

\(at | ot\)

r

role

t =

\(17\)

πϕ \(a

The purpose of the offline pre-training phase is to extract old

t | ot\)

effective driving priors from the InD dataset, providing a We further enhance training with adam optimizer and high-quality model initialization for the online phase. As gradient clipping. These stabilizing techniques enable robust shown in Fig. 4, which displays the changes in the critic fine-tuning and effective adaptation to dynamic, multi-agent networks’ Q1 and Q2 losses and the reward improvement environments. 

metric during offline training, we can observe the learning IV. EXPERIMENTS AND ANALYSIS

progress. The loss values steadily converge as training progresses, indicating that the critic network effectively learned Experiments were conducted using the CARLA simula-state-action value relationships from the offline data and that tor paired with Unreal Engine in synchronous mode. The the training process possessed good stability. Furthermore, primary scenario involves one intersection within CARLA’s the reward improvement metric eventually stabilizes around Town03 map \(shown in Fig. 3\). In this simulation scenario, 112%, exceeding the 100% baseline. This demonstrates that a total of 5 vehicles are present: a variable number \(1 to the policy learned via CQL combined with BC outperforms 3\) CAVs, designated "red", are controlled by the proposed the average behavior present in the dataset in terms of system, while the remaining background vehicles, designated optimizing the offline reward objective, successfully learning

"blue", are managed by CARLA’s Traffic Manager. Addition-strategies beyond mere imitation, and providing a quality ally, up to 3 pedestrians are randomly spawned on sidewalks initialization basis for online fine-tuning. 

and programmed to cross the road. A real intersection map based on the Institute of Science Tokyo campus was utilized C. Online Training Results

for generalization testing. We assume the RSU possesses BEV perception and performs inference using the decision To validate the effectiveness of online fine-tuning and model obtained after online fine-tuning to determine driving the value of offline pre-training, we compare the training strategies, subsequently sending control signals to the CAVs progress of our proposed hybrid method against the online-via simulated V2I communication. 

only baseline. Fig. 5 presents the convergence curves for both

TABLE I: Performance comparison summary Method / Scenario

Failure rate \(%\)

Avg. time \(s\)

Ours \(1 Agent, Town03\)

0.01

5.52

Ours \(2 Agent, Town03\)

0.03

5.49

Ours \(3 Agent, Town03\)

0.02

5.25

Autoware \(1 Agent, Town03\)

5.31

5.77

Ours \(3 Agent, Real Map\)

0.02

5.15

\(a\)

\(a\)

\(b\)

\(b\)

Fig. 6: Final model performance evaluation results \(a\) suc-Fig. 5: Comparison of online training w/ and w/o offline RL, cess rate by testing episodes, \(b\) average travel time by \(a\) reward, \(b\) success rate. 

testing episodes

average episode reward and success rate during the external map. When controlling a single vehicle, the failure rate was online training phase for both methods. 

0.01%. Compared to the 5.31% failure rate exhibited by the As shown in Fig. 5, our proposed hybrid method, lever-Autoware baseline in the identical single-vehicle scenario, aging the pre-trained model, exhibits a much higher initial our single-agent controller shows higher performance. 

average episode reward compared to the online-only method Notably, despite the significant increase in coordination starting from scratch. Furthermore, the hybrid approach complexity when scaling from single- to multi-vehicle sce-converges more rapidly to its final reward level, indicating narios, our system did not exhibit a marked decline in that offline pre-training significantly accelerates the online success rate. Specifically, failure rate was 0.03% in the two-learning process and contributes to achieving strong final vehicle coordination scenario and decreased to 0.02% in the performance. Additionally, the convergence trend for success three-vehicle coordination scenario. The combination of the rate mirrors that of the reward. Our proposed method reaches RSU’s BEV perspective and the self-attention mechanism high success rates considerably faster, whereas the online-contributes to this robustness, demonstrating our method’s only method requires significantly more training episodes to effectiveness in handling complex multi-agent cooperative approach similar levels of reliability. This comparison further tasks. 

demonstrates that offline pre-training markedly enhances As shown in Fig. 6 and Tab. I, the traffic efficiency both the efficiency of the online learning phase and the results indicate that our method also demonstrated strong robustness of the ultimately learned policy. 

performance. The average travel time in the single-vehicle scenario was 5.52 seconds, outperforming the 5.77 seconds D. Final Model Performance Evaluation and Generalization recorded by the Autoware baseline. As the number of con-Analysis

trolled vehicles increased, the average travel time showed We evaluated the model through 10,000 performance test a slight downward trend: 5.49 seconds for the two-vehicle episodes on both the Town03 intersection and the custom scenario and 5.25 seconds for the three-vehicle scenario. 

map, comparing it against baselines. A summary of key This indicates that the multiple RL agents coordinated by performance indicator comparisons is shown in Fig. 6 and our system formed a highly effective collaborative passage Tab. I. The proposed algorithmic model demonstrates high pattern. Their interactions proved more efficient than those safety and reliability across all test scenarios on the Town03

with a larger number of background vehicles controlled by

the Traffic Manager. 

\[11\] M. Gallo, “Combined optimisation of traffic light control parameters Finally, in the generalization test, the three-vehicle model and autonomous vehicle routes,” Smart Cities, vol. 7, no. 3, pp. 1060–

1088, 2024. 

trained in Town03 was deployed on the real intersection map. 

\[12\] M. Ghadi, “A grid-based framework for managing autonomous vehi-The model achieved an extremely low failure rate of 0.02%

cles’ movement at intersections,” Periodica Polytechnica Transporta-and an average travel time of 5.15 seconds in this novel tion Engineering, vol. 52, no. 3, pp. 235–245, 2024. 

\[13\] Y. Shi, H. Dong, C. He, Y. Chen, and Z. Song, “Mixed vehicle environment. This suggests that the expanded collective field platoon forming: A multi-agent reinforcement learning approach,” 

of view inherent in the three-vehicle setup mitigated the IEEE Internet of Things Journal, vol. PP, pp. 1–1, 01 2025. 

impact of individual visual blind spots. Furthermore, as this

\[14\] H. Taghavifar, C. Hu, C. Wei, A. Mohammadzadeh, and C. Zhang, 

“Behaviorally-aware multi-agent rl with dynamic optimization for map featured shorter traversal distance, it enabled our system autonomous driving,” IEEE Transactions on Automation Science and to operate more smoothly and efficiently. This result strongly Engineering, vol. PP, pp. 1–1, 01 2025. 

validates the excellent generalization capability of the learned

\[15\] Y. Zhang, R. Hao, T. Zhang, X. Chang, Z. Xie, and Q. Zhang, “A trajectory optimization-based intersection coordination framework for policy, showcasing its adaptability to different environmental cooperative autonomous vehicles,” IEEE Transactions on Intelligent characteristics and providing a solid foundation for the Transportation Systems, vol. 23, no. 9, pp. 14 674–14 688, 2021. 

practical application of the method. 

\[16\] S. Iqbal and F. Sha, “Actor-attention-critic for multi-agent reinforcement learning,” arXiv preprint arXiv:1810.02912, 2019, iCML 2019

camera ready version. 

V. CONCLUSION AND FUTURE WORKS

\[17\] R. Younas, H. M. Raza Ur Rehman, I. Lee, B.-W. On, S. Yi, and G. S. 

Choi, “Sa-marl: Novel self-attention-based multi-agent reinforcement This research addresses the complex coordination chal-learning with stochastic gradient descent,” IEEE Access, vol. 13, pp. 

lenges at unsignalized intersections by proposing an RSU-35 674–35 687, 2025. 

based centralized cooperative driving framework. The frame-

\[18\] W.-C. Tseng, T.-H. J. Wang, Y.-C. Lin, and P. Isola, “Offline multi-agent reinforcement learning with knowledge distillation,” in Advances work employs a two-stage method to train the decision in Neural Information Processing Systems, vol. 35. Curran Associates, model: offline pre-training initializes policies, followed by Inc., 2022, pp. 226–237. 

online fine-tuning in the simulation environment. Extensive

\[19\] Z. Li, F. Nie, Q. Sun, F. Da, and H. Zhao, “Boosting offline reinforcement learning for autonomous driving with hierarchical latent skills,” 

experiments demonstrate the method’s effectiveness, achievin 2024 IEEE International Conference on Robotics and Automation ing high success rate and strong coordination robustness in \(ICRA\), 2024, pp. 18 362–18 369. 

scenarios with up to three controlled vehicles. Future primary

\[20\] Z. Wang, G. Wu, and M. J. Barth, “Cooperative eco-driving at signalized intersections in a partially connected and automated ve-work involves the proof-of-concept \(PoC\) experiments to hicle environment,” IEEE Transactions on Intelligent Transportation fully validate the system effectiveness in the real world. 

Systems, vol. 21, no. 5, pp. 2029–2038, 2019. 

\[21\] Z. Wang, K. Han, and P. Tiwari, “Digital twin-assisted cooperative R

driving at non-signalized intersections,” IEEE Transactions on Intelli-EFERENCES

gent Vehicles, vol. 7, no. 2, pp. 198–209, 2021. 

\[22\] K. Wang, Z. Li, K. Nonomura, T. Yu, K. Sakaguchi, O. Hashash, and

\[1\] K. F. Chu, A. Lam, and V. Li, “Traffic signal control using end-to-W. Saad, “Smart mobility digital twin based automated vehicle navi-end off-policy deep reinforcement learning,” IEEE Transactions on gation system: A proof of concept,” IEEE Transactions on Intelligent Intelligent Transportation Systems, vol. PP, pp. 1–12, 2021. 

Vehicles, pp. 1–14, 2024. 

\[2\] U.S. Department of Transportation, Federal Highway Administration. 

\[23\] K. Wang, T. Yu, Z. Li, K. Sakaguchi, O. Hashash, and W. Saad, “Dig-

\(2024, August\) Mire 2.1: Model inventory of roadway elements. Re-ital twins for autonomous driving: A comprehensive implementation port No. FHWA-SA-24-052. \[Online\]. Available: https://highways.dot. 

and demonstration,” in 2024 International Conference on Information

gov/sites/fhwa.dot.gov/files/2024-08/MIRE\_2.1\_FINAL\_508v3.pdf

Networking \(ICOIN\), 2024, pp. 452–457. 

\[3\] National Highway Traffic Safety Administration. \(2024, April\) Nhtsa

\[24\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, estimates 39,345 traffic fatalities in 2024. U.S. Department of

“CARLA: An open urban driving simulator,” in Proceedings of the Transportation. \[Online\]. Available: https://nhtsa.gov/press-releases/

1st Annual Conference on Robot Learning, 2017, pp. 1–16. 

nhtsa-2023-traffic-fatalities-2024-estimates

\[25\] J. Bock, R. Krajewski, T. Moers, S. Runde, L. Vater, and L. Eckstein, 

\[4\] S. Chen, X. Hu, J. Zhao, R. Wang, and M. Qiao, “A review of

“The ind dataset: A drone dataset of naturalistic road user trajectories decision-making and planning for autonomous vehicles in intersection at german intersections,” in 2020 IEEE Intelligent Vehicles Symposium environments,” World Electric Vehicle Journal, vol. 15, no. 3, p. 99, \(IV\), 2020, pp. 1929–1934. 

2024. 

\[26\] A. Kumar, A. Zhou, G. Tucker, and S. Levine, “Conservative q-

\[5\] K. Wang, C. She, Z. Li, T. Yu, Y. Li, and K. Sakaguchi, “Roadside learning for offline reinforcement learning,” in Advances in Neural units assisted localized automated vehicle maneuvering: An offline Information Processing Systems, vol. 33. 

Curran Associates, Inc., 

reinforcement learning approach,” in 2024 IEEE 27th International 2020, pp. 1179–1191. 

Conference on Intelligent Transportation Systems \(ITSC\), 2024, pp. 

\[27\] D. A. Pomerleau, “Alvinn: An autonomous land vehicle in a neural 1709–1715. 

network,” in Advances in Neural Information Processing Systems, 

\[6\] Z. Li, K. Wang, T. Yu, and K. Sakaguchi, “Het-SDVN: SDN-based vol. 1. 

Morgan-Kaufmann, 1988. 

radio resource management of heterogeneous V2X for cooperative

\[28\] C. Yu, A. Velu, E. Vinitsky, J. Gao, Y. Wang, A. Bayen, perception,” IEEE Access, vol. 11, pp. 76 255–76 268, 2023. 

and Y. Wu, “The surprising effectiveness of ppo in cooperative, 

\[7\] D. Suo, B. Mo, J. Zhao, and S. E. Sarma, “Proof of travel for trust-multi-agent games,” arXiv preprint arXiv:2103.01955, 2021, accepted based data validation in V2I communication,” IEEE Internet of Things at NeurIPS 2022 Datasets and Benchmarks. \[Online\]. Available: Journal, vol. 10, no. 11, pp. 9565–9584, 2023. 

https://arxiv.org/abs/2103.01955

\[8\] H. Alemayehu and A. Sargolzaei, “Testing and verification of con-

\[29\] Autoware. \[Online\]. Available: https://autoware.org/. 

nected and autonomous vehicles: A review,” Electronics, vol. 14, no. 3, p. 600, 2025. 

\[9\] F. Sana, N. L. Azad, and K. Raahemiar, “Autonomous vehicle decision-making and control in complex and unconventional scenarios—a review,” Machines, vol. 11, no. 7, p. 676, 2023. 

\[10\] Y. Zhu, Z. He, and G. Li, “A bi-hierarchical game-theoretic approach for network-wide traffic signal control using trip-based data,” IEEE

Transactions on Intelligent Transportation Systems, vol. 23, no. 9, pp. 

15 408–15 419, 2022. 


# Document Outline

+ Introduction 
+ RSU-CAVs Cooperative System 
+ Hybrid Reinforcement Learning Framework  
	+ Observation Space 
	+ Action Space 
	+ Reward Function 
	+ Offline Pre-training: Networks and Algorithm 
	+ Online Fine-tuning: Networks and Algorithm 

+ Experiments and Analysis  
	+ Baselines and Evaluation Metrics 
	+ Offline Pre-training Results 
	+ Online Training Results 
	+ Final Model Performance Evaluation and Generalization Analysis 

+ Conclusion and Future Works 
+ References



