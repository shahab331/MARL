Large-Scale Mixed-Traffic and Intersection Control using Multi-agent Reinforcement Learning

Songyang Liu1, Muyang Fan2, Weizi Li3, Jing Du1, Shuai Li1

Abstract— Traffic congestion remains a significant challenge have demonstrated the feasibility of using image data rather in modern urban networks. Autonomous driving technolo-than detailed traffic measurements for RL-based control \[7\], gies have emerged as a potential solution. Among traffic developed RL frameworks incorporating real-world driving control methods, reinforcement learning has shown superior profiles to enhance safety, stability, and efficiency in mixed performance over traffic signals in various scenarios. However, prior research has largely focused on small-scale networks or traffic scenarios \[8\], \[9\], and provided evidence that RL-isolated intersections, leaving large-scale mixed traffic control based techniques can reduce collisions and improve overall largely unexplored. This study presents the first attempt to use urban traffic flow \[10\], \[11\]. Despite these advancements, ex-decentralized multi-agent reinforcement learning for large-scale isting research has been limited to small-scale settings, with mixed traffic control in which some intersections are managed little exploration of large-scale mixed-traffic control where by traffic signals and others by robot vehicles. Evaluating a real-world network in Colorado Springs, CO, USA with 14 inter-traffic signals and RVs operate together. Recent multi-agent sections, we measure traffic efficiency via average waiting time frameworks \[12\] and control methods for mixed traffic \[11\]

of vehicles at intersections and the number of vehicles reaching suggest that integrating these approaches may be feasible, their destinations within a time window \(i.e., throughput\). At yet a solution for large-scale traffic remains unexplored. 

80% RV penetration rate, our method reduces waiting time We present the first attempt of applying decentralized from 6.17 s to 5.09 s and increases throughput from 454 vehicles per 500 seconds to 493 vehicles per 500 seconds, outperforming multi-agent reinforcement learning \(MARL\) for large-scale the baseline of fully signalized intersections. These findings mixed-traffic and intersection control, in which traffic signals suggest that integrating reinforcement learning-based control govern some intersections while RL-controlled RVs regulate large-scale traffic can improve overall efficiency and may inform the others. Unlike previous studies that focus exclusively on future urban planning strategies. 

solely signalized or unsignalized control, we investigate how I. INTRODUCTION

RVs and traffic signals can coexist to optimize urban mo-Traffic congestion remains a major issue in modern urban bility. Using our MARL-based control method, RVs adjust systems. In 2024, it caused drivers to lose an average of 43

their behavior dynamically based on local traffic conditions, hours in traffic, costing $771 in lost time and productivity. 

offering a flexible alternative to static traffic signals. 

New York City, Chicago \(both 102 hours\), and Los Angeles We conduct experiments on a large-scale network of 14 in-

\(88 hours\) were the most congested U.S. cities, costing tersections using the Simulation of Urban MObility \(SUMO\) drivers $1,826 and $1,575, respectively \[1\]. Similarly, Lon-

\[13\]. To evaluate our approach, we test five configurations don drivers faced 101 hours of congestion in 2024, costing of 14 intersections. Each configuration divides the 14 inter-the city $4.88 billion, or $1,193 per driver \[2\]. These figures sections into a set of unsignalized intersections controlled by highlight congestion’s prevalence and high costs worldwide. 

RL-driven RVs and a set of signalized intersections that are Autonomous driving technologies have been explored to regulated by traffic lights. We compare this mixed-control alleviate congestion. Rapid progress has led to more vehicles approach with a baseline where all intersections rely solely being equipped with autonomous features and tested in real-on traffic signals. We evaluate traffic performance using arXiv:2504.04691v1 \[cs.LG\] 7 Apr 2025

world conditions. Nevertheless, the shift toward full trans-two metrics: 1\) average waiting time W , which measures portation autonomy is expected to experience a prolonged traffic efficiency by averaging the total time vehicles remain period in which human-operated vehicles \(HVs\) and robot motionless near an intersection \[4\], \[14\], \[15\], and 2\) vehicle vehicles \(RVs\) cooperate, hence mixed traffic. 

throughput Q, which represents the number of vehicles Traffic control methods have also seen significant progress crossing an intersection or reaching their destinations over in recent years. In particular, Reinforcement learning \(RL\)-

the second half of an episode \(500 seconds\). The most based vehicle control methods have been shown to outper-significant improvement over the baseline is observed when form traffic signals at complex intersections \[3\]–\[6\]. Studies the RV penetration rate reaches 80%: W reduces from 6.17 s to 5.09 s \(a 20% deduction\) and Q increases from 454

1Songyang Liu, Jing Du, and Shuai Li are with Department of Civil vehicles per 500 seconds \(v/500s\) to 493 v/500s \(a 9%

and Coastal Engineering at University of Florida, Gainesville, FL, USA improvement\). 

liusongyang@ufl.edu; eric.du@essie.ufl.edu; 

shuai.li@ufl.edu

By bridging the gap between fully signalized and 2Muyang Fan is with Department of Computer Science at University of autonomous traffic control, this study introduces a new Memphis, Memphis, TN, USA mfan1@memphis.edu

paradigm for urban traffic management. As trends in 3Weizi Li is with Min H. Kao Department of Electrical Engineering and Computer Science at University of Tennessee, Knoxville, TN, USA autonomous transportation continue, our findings may weizili@utk.edu

inform urban planning strategies by showing that mixed-

traffic control can improve efficiency while reducing policy exploration improves sample efficiency, while tech-reliance on static signals. This work is an initial step niques such as value distribution estimation and skill-based toward understanding the feasibility and effectiveness learning contribute to the stability of RL-based control. 

of a large-scale transition to signal-free intersections in Decentralized multi-agent RL has been shown to substan-real-world networks. The Code of our work is available tially reduce waiting times at complex unsignalized intersec-at https://github.com/cgchrfchscyrh/MixedTrafficControl\_IROS. tions, particularly when there is a high presence of RVs \[4\], 

\[36\]. One study proposed a decentralized RL framework for large-scale traffic signal management leveraging localized II. RELATED WORK

optimization and indirect collaboration through shared state information \[37\], while another extended RL coordination to Managing urban intersections has become increasingly city-wide mixed traffic networks by incorporating dynamic challenging as autonomous and human-driven vehicles con-vehicle routing and privacy-preserving crowdsourcing to bal-tinue to share the roads. Existing traffic control techniques, ance RV penetration and mitigate localized congestion \[36\]. 

such as fixed-time and actuated signaling have been exten-Unlike earlier approaches that depend on either traffic lights sively implemented to regulate traffic under stable condi-or full autonomous coordination, our method explores how tions \[16\], \[17\]. However, these methods often struggle to both systems can operate together to optimize urban mobility. 

cope with the dynamic and complex nature of modern traffic environments \[18\]. Meanwhile, optimization-based meth-III. METHODOLOGY

ods, including integer linear programming and rule-based strategies, can improve efficiency but encounter scalability We first explain our mixed control method at intersections. 

issues when applied to expansive networks \[19\]. In contrast, Second, we introduce our vehicle behavior modeling method, learning-based control methods can dynamically adapt to followed by the implementation details of our method. 

changing traffic conditions, optimizing vehicle movement in Lastly, we introduce the evaluation metrics of our approach. 

real time. Following this approach, we develop an RL-based A. RL-based Control for Mixed Traffic at Intersections vehicle control strategy to enhance traffic efficiency. 

Various studies have focused on controlling traffic at We address the challenge of coordinating mixed traffic unsignalized intersections, especially for connected and au-at unsignalized intersections by formulating the task as a tonomous vehicles \(CAVs\). For example, an early study Partially Observable Markov Decision Process \(POMDP\): proposed a multi-agent control system in which CAVs se-cure space-time reservations on a first-come, first-served \(S, A, T, R, O, Z, µ0, γ\), 

basis \[20\]. Building on this idea, another study applied the where

FCFS scheduling strategy to CAV platoons \[21\], and a controllable gap method was introduced that dynamically adjusts

• S is the set of all possible states; 

the time intervals between vehicles—accounting for their

• A is the set of actions available to the vehicles; speeds and potential conflicts to reduce collision risks \[22\]. 

• T \(s′ | s, a\) denotes the probability of transitioning from Additional research has explored decentralized approaches, state s to state s′ when action a is taken; 

such as consensus-based trajectory management \[23\] and

• R\(s, a\) is the reward function providing feedback for a energy optimization techniques \[24\], although these meth-given state-action pair; 

ods typically assume an environment composed entirely of

• O represents the observation space corresponding to the autonomous vehicles. In addition, these approaches are based partial view of the environment available to each RV; on the assumption that all vehicles are connected, which

• Z\(o | s\) gives the likelihood of obtaining observation o does not hold in mixed-traffic conditions where HVs lack when the true state is s; 

connectivity. Hence, our method assumes only RVs can

• µ0 is the distribution of the initial state; and exchange traffic information within a range of intersections, 

• γ is the discount factor applied to future rewards. 

allowing for a more realistic and adaptable control strategy. 

At each discrete time step t, an RV selects an action Recent studies suggest that RL can enable RVs to in-at ∈ A according to a policy πθ\(at | st\). Upon taking fluence HVs and optimize traffic efficiency \[3\], \[4\], \[7\], this action, the environment updates to a new state st\+1 and

\[25\]–\[30\], indicating that RV-based control can outperform the RV receives an immediate reward rt. In our multi-agent traffic signals at unsignalized intersections \[3\], \[4\]. Sev-setting, all RVs share the same policy while making decisions eral studies demonstrate that RL-driven control—whether independently. We seek to maximize the overall discounted through decision-making models \[31\] or multi-task strate-reward Gt, which sums the immediate rewards from time t gies \[32\]—can outperform traffic signals in unsignalized to T , each multiplied by a discount factor γ j−t. 

settings. Moreover, studies focusing on efficient RL meth-Each RV is faced with a binary decision Stop or Go. 

ods \[33\] and curriculum-based approaches \[34\], along with The Stop command prevents the vehicle from entering the enhanced strategies for urban traffic scenarios \[35\], have intersection, whereas the Go command permits it to continue shown promising improvements in convergence and perfor-moving. At time t, the observation vector ot that a RV

mance. Specifically, leveraging expert priors and structured receives is structured as

all 14 intersections being managed by traffic signals. This M

M

ot =

⟨qd, τd⟩

σd, 

\(1\)

design enables the study of the impact of shifting control d∈D

d∈D

from traffic signals to RVs on large-scale traffic. 

where D represents the set of all traffic directions, while qd D. Evaluation Metrics

denotes the number of vehicles queued in a specific direc-We assess traffic performance using the following metrics. 

tion d. The variable τd corresponds to the average waiting 1\) Average Waiting Time \(W \): This metric has been time of vehicles arriving from direction d, and σd indicates adopted frequently to evaluate traffic efficiency over a road whether vehicles from direction d are currently occupying network \[4\], \[14\], \[15\]. For each vehicle, the waiting time the intersection. 

is defined as the total duration it remains motionless within To promote efficient traffic flow and mitigate potential the control zone. To compute this metric, we first determine conflicts, we design a reward function that blends local the average waiting time for a specific moving direction performance with a penalty for conflicts. Specifically, when by averaging the waiting times of all vehicles traveling in vehicles approaching from conflicting directions converge at that direction; similarly, for an intersection, we average the the intersection, priority is assigned based on a weighted waiting times of all vehicles present. W is computed by measure of the queue length and waiting time. The reward adding up every vehicle’s waiting time and then dividing received at time t is defined as

that sum by the number of vehicles. This metric serves as an indicator of traffic efficiency, with lower values reflecting rt = β · rlocal \+ rpenalty, 

t

t

\(2\)

improved flow and reduced congestion. 

where β is a scaling constant. At each time step, the local 2\) Vehicle Throughput \(Q\): Vehicle throughput is defined reward is determined by the vehicle’s action. If the vehicle differently at the individual intersection level and the network executes Go, it receives a reward equal to τd, the average level. For a single intersection, Q represents the number waiting time for the relevant direction. If it instead chooses of vehicles that successfully pass that intersection. For an Stop, it receives a penalty of −τd. In addition, if a conflict entire network, Q refers to the total number of vehicles occurs at the intersection, the vehicle incurs a penalty of −1; that reach their designated destinations. This metric provides otherwise, there is no penalty. 

insight into both localized traffic efficiency at intersections and overall traffic performance network-wide. The higher B. Vehicle Behavior Modeling

the throughput, the smoother the traffic flow and better the HVs are simulated using the Intelligent Driver Model system optimization. 

\(IDM\) \[38\], which calculates acceleration based on the current traffic environment. In contrast, RVs employ a hybrid IV. EXPERIMENTS AND RESULTS

strategy: they follow IDM rules when they are more than 30

We first explain our experiment set-up, then the traffic per-meters away from the intersection, and switch to a learned formance at individual intersections and the entire network. 

control policy once they are within the intersection zone. 

When the learned policy directs an RV to Go, the vehicle A. Experiment Set-up

accelerates at its maximum allowable rate. However, if the Our simulation network shown in Fig. 1 is constructed policy mandates Stop, the vehicle decelerates in a manner using intersection data from the city of Colorado Springs, that depends on its current speed v and the distance remain-CO, USA. The network features 12 peripheral entrances ing to the intersection, denoted as dint. The deceleration is and exits \(where origin-destination pairs are defined\) and calculated as −v2/2 dint, where v is the current speed of 14 intersections. We experiment with various configurations vehicle, and dint is the distance to the intersection. 

by designating a subset of intersections \(i.e., 2, 4, 6, 8, or 10\) to be managed by RVs, while the remaining intersections C. Mixed Control of Intersections

operate under traffic signals. 

We implement two distinct approaches to intersection For training our RL policy, we employ the Rainbow control: one that uses RL-controlled RV coordination and the DQN algorithm \[39\] over 1,000 iterations. We vary the RV

other that relies on traffic signals. At intersections managed penetration rates from 40% to 80% in 10% increments, with by RVs, the traffic lights are disabled, enabling RVs to reg-each setting requiring between 10 to 30 hours of training ulate traffic. Our study investigates how these two methods using 16 CPU cores from an AMD EPYC 7742 Processor can coexist within a large-scale traffic network to optimize and an NVIDIA A100 graphics card. The prioritized replay urban mobility. 

buffer parameter α is set to 0.5, with a replay buffer capacity We evaluate five configurations, denoted as xU \+ yS, of 50,000. The algorithm utilizes 51 atoms and a neural where x is the number of intersections controlled by RVs network with three hidden layers of 512 neurons each. A and y is the number regulated by traffic signals, x ∈

discount factor of 0.99 is applied to prioritize long-term

\{0, 2, 4, 6, 8, 10\}, y ∈ \{14, 12, 10, 8, 6, 4\}, totaling 14 inter-rewards, while a mini-batch size of 32 is used for training sections. For example, in the 2U \+ 12S setup, two inter-updates. The learning rate is set at 0.0005 to control the sections are managed by RVs and 12 by traffic signals. For step size during optimization. Additionally, the control zone comparison, the baseline configuration 0U \+ 14S represents radius is defined as 30 meters, determining the spatial range



average waiting time is consistently lower across all control configurations and RV penetration rates, with intersection 1

achieving waiting times up to 10 times lower than the baseline; however, in some cases the vehicle throughput, although increasing with higher RV rates, remains slightly below the baseline. At intersections 3 and 5, high RV penetration of 60% and 80% respectively ensures that waiting times are better than the baseline across all configurations, yet throughput, despite rising with RV rate, still falls marginally short of the baseline level. In contrast, intersections 2, 4, 7, 9, 10, 12, and 13 show mixed waiting time performance, with some control configurations outperforming the baseline and Fig. 1: We study a large-scale network that consists of 14 inter-others not. Notably, intersection 10 only exhibits improved sections in Colorado Springs, CO, USA. Four intersections \(i.e., 5, waiting time under the 10U \+ 4S configuration, although its 7, 9, and 11\) are shown in close-up views as examples. 

throughput is consistently higher than the baseline across all scenarios. Furthermore, intersections 4, 9, 12, and 13

for decision-making in the environment. After training, each generally achieve higher throughput than the baseline; for RL policy is evaluated 100 times, and the results are reported instance, intersection 9 shows throughput that increases with using the values over these 100 evaluations, in which each RV rate and ultimately exceeds the baseline, even as waiting evaluation runs for a 1000-second simulation period. 

time improvements vary. Overall, while advanced control strategies tend to reduce waiting times at most intersections, B. Overall Results

the corresponding gains in vehicle throughput are less uni-In Fig. 2, the average waiting time and vehicle throughput form, reflecting a complex interplay between local traffic are analyzed for the 8U \+ 6S and 4U \+ 10S configurations dynamics and control configuration. 

across the entire network. In the 8U \+ 6S setup, our method consistently outperforms the baseline across all five RV

C. Results At Various RV Rates

penetration rates for both metrics. The waiting time decreases at 40%, 60%, and 80%, while 50% and 70% show higher Tables I and II show the results of traffic performance at values. Similarly, throughput improves at 40%, 60%, and the 14 intersections and the entire network under six network 80%, but declines at 50% and 70%. In the 4U \+ 10S

control configurations at RV rate 50% and 80%, respectively. 

configuration, the method reduces waiting time significantly In each table, rows 1–14 show individual intersection results, at an 80% RV rate and improves throughput when the RV

while the last row reports the entire network results. 

rate exceeds 40%. Waiting time decreases at 40%, 50%, 60%, When the RV rate is at 50%, the configurations 2U \+

and 80%, but increases at 70%. Throughput follows a similar 12S and 8U \+ 6S achieve lower network W and higher trend, rising at 40%, 50%, 60%, and 80%, while declining network Q, while 4U \+ 10S, 6U \+ 8S and 10U \+ 4S get at 70%. For overall network performance across all five higher W and higher Q compared to the baseline 0U \+ 14S. 

configurations, the average waiting time W generally reduces Over the entire network, the highest improvement \(bold as the RV penetration rate increases from 40% to 80%, indi-values in the Table\) for the two metrics occur at 2U \+ 12S

cating improved traffic efficiency. The vehicle throughput Q

and 10U \+ 4S configuration. Our method impacts individual increases across all configurations, suggesting more vehicles intersections differently: some achieve lower W and oth-successfully reach their destinations. The most significant ers experience higher W . For intersection 6, the highest improvement is observed in the 8U \+ 6S configuration when improvement happens with an 98.04% reduction in W . 

RV rate = 80%, where W is reduced from 6.17 s to 5.09 s, 2U \+ 12S and 8U \+ 6S outperform the baseline with waiting and Q increases from 454 v/500s to 493 v/500s, compared times of 5.86 s and 6.11 s and throughput of 470 v/500s and to the baseline \(0U \+ 14S\). This suggests that controlling 471 v/500s, respectively, but the 6U \+ 8S and 10U \+ 4S

some intersections with RVs while keeping others managed configurations exhibit increased waiting times \(7.92 s and by traffic signals improves overall traffic performance when 7.02 s\) despite moderate throughput gains. 

the RV rate is high enough. 

When the RV rate reaches 80%, the 8U \+ 6S configura-Fig. 3 shows the average waiting time W for 14 inter-tion achieves the best performance overall with an average sections when RV rate = 50% and 80%. At 50% RV rate, waiting time of 5.09 s and throughput of 493 v/500s, nine intersections achieve lower W than traffic light control, while 2U \+ 12S, 4U \+ 10S and 10U \+ 4S also improve increasing to 11 intersections at 80% RV rate. These results waiting times and throughput compared to the baseline. For demonstrate that our method reduces vehicle waiting times the network, the highest improvements for the two metrics, at most intersections and improves as the RV rate rises. 

both occur at 8U \+6S configuration. Our method still impacts At each individual intersection, our method’s performance individual intersections differently: some achieve lower W

varies, and the analysis of all 14 intersections reveals several and the others experience higher W . For intersection 6, the trends. To start with, at intersections 1, 6, 8, 11, and 14, the highest improvement occurs with an 98.43% reduction in W . 

Intersection control configuration Intersection

0U \+ 14S \(baseline\)

2U \+ 12S

4U \+ 10S

6U \+ 8S

8U \+ 6S

10U \+ 4S

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

1

5.27

391

0.53

349

0.67

346

0.67

346

0.6

351

0.63

355

2

3.07

194

4.92

190

4.97

191

17.47

170

6.9

192

16.4

178

3

7.26

464

7.12

362

6.24

373

8.63

332

7.41

367

7.15

371

4

0.95

56

2.49

64

2.5

64

6.2

56

0.81

65

6.42

61

5

9.74

515

9.65

504

11.55

407

11.62

386

11.47

396

11.82

382

6

5.10

88

3.03

87

4.41

86

4.37

89

0.11

102

0.1

108

7

12.89

488

13.22

490

20.47

396

21.92

367

19.98

388

18.31

393

8

7.62

198

6.76

182

7.24

184

7.3

184

4.2

177

4.97

177

9

1.91

190

2.04

188

2.0

191

1.95

191

2.02

191

1.96

192

10

0.28

39

0.35

44

0.37

43

0.36

41

0.4

43

0.01

44

11

17.83

144

15.91

143

16.81

138

16.36

143

16.45

145

16.6

141

12

0.79

112

0.78

114

0.81

117

0.8

118

1.1

121

0.15

128

13

4.19

221

4.94

230

5.03

233

4.94

235

5.2

235

5.49

236

14

9.49

354

8.24

358

8.47

359

8.2

358

8.21

363

8.4

362

Network

6.17

454

5.86

470

6.63

459

7.92

448

6.11

471

7.02

473

TABLE I: Average waiting time W and vehicle throughput Q for 14 individual intersections and entire network under six different network control configurations when RV rate = 50%. Rows 1-14 show individual intersection data, while the last row represents the entire network’s data. For a single intersection, Q represents the number of vehicles that successfully leave this intersection. For the entire network, Q refers to the total number of vehicles that reach their designated destinations. Increasing the number of unsignalized intersections leads to variable performance. The configurations 2U \+ 12S and 8U \+ 6S achieve lower network W and higher network Q, while 4U \+ 10S, 6U \+ 8S and 10U \+ 4S get higher W and higher Q compared to the baseline 0U \+ 14S. For the network, bold values indicate the highest improvement for the two metrics, occurring at 2U \+ 12S and 10U \+ 4S configuration. Our method impacts individual intersections differently: some achieve lower W and others experience higher W . For intersection 6, bold value indicates the highest improvement with an 98.04% reduction in W . 2U \+ 12S achieves the lowest W of 5.86 s across the entire network and has the lowest W at six of the 14 intersections, making it the best configuration for minimizing delays. For Q, 10U \+ 4S achieves the highest network-wide value of 473 v/500s and has the highest Q at six intersections, while the baseline ranks second with four intersections. 

These results indicate that 10U \+ 4S is the best configuration for maximizing throughput. 

Intersection control configuration

Intersection

0U \+ 14S \(baseline\)

2U \+ 12S

4U \+ 10S

6U \+ 8S

8U \+ 6S

10U \+ 4S

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

1

5.27

391

0.46

359

0.74

365

0.77

364

0.75

365

0.75

364

2

3.07

194

4.83

190

4.94

191

8.46

190

0.23

212

0.69

206

3

7.26

464

3.89

430

5.26

419

6.11

398

5.57

408

6.9

378

4

0.95

56

2.55

64

2.46

63

0.67

64

0.06

65

1.32

67

5

9.74

515

10.64

493

8.93

435

8.4

419

8.83

437

10.98

405

6

5.10

88

4.5

86

4.3

87

4.29

87

0.08

99

0.11

106

7

12.89

488

13.87

490

16.08

431

16.81

419

15.76

432

18.37

420

8

7.62

198

6.79

182

6.8

187

7.32

188

3.8

184

4.18

179

9

1.91

190

2.05

190

2.04

190

2.03

192

2.11

190

2.06

190

10

0.28

39

0.39

45

0.36

43

0.38

42

0.4

43

0.01

44

11

17.83

144

16.51

137

16.26

144

17.11

141

17.47

139

17.24

139

12

0.79

112

0.77

113

0.82

118

0.82

118

1.13

119

0.13

126

13

4.19

221

4.88

229

4.99

233

4.98

230

5.23

233

5.57

235

14

9.49

354

8.01

357

8.14

359

8.29

358

8.28

364

8.32

361

Network

6.17

454

5.76

473

5.91

466

6.31

475

5.09

493

5.95

478

TABLE II: Average waiting time W \(s\) and vehicle throughput Q \(v/500s\) for 14 individual intersections and entire network when RV rate = 80%. The configurations 2U \+ 12S, 4U \+ 10S, 8U \+ 6S, and 10U \+ 4S achieve lower network W and higher network Q, while 6U \+ 8S gets higher W and higher Q compared to the baseline 0U \+ 14S. For the entire network, the highest improvement for W

and Q both occur at 8U \+ 6S configuration. For intersection 6, the highest improvement occur with an 98.43% reduction in W . 8U \+ 6S

achieves the lowest W of 5.09 s across the entire network and has the lowest W at four of the 14 intersections, while the baseline and 2U \+ 12S rank second with three intersections at the same time. These results make 8U \+ 6S the best configuration for minimizing delays when RV rate = 80%. For Q, 8U \+ 6S also achieves the highest network-wide value of 493 v/500s and has the highest Q at two intersections, while the 10U \+ 4S ranks first with four intersections. These results indicate that 8U \+ 6S is the best configuration for maximizing network-wide throughput. 

We also conduct similar experiments when RV rate = 40%, 454 v/500s, although the degree varies. The 2U \+ 12S

60% and 70%. At the 40% RV rate, most configurations configuration reduces waiting time to 5.89 s and increases improve performance relative to the baseline of 6.17 and throughput to 474 v/500s, while the 8U \+ 6S setup fur-





Fig. 2: Average waiting time W \(s\) and vehicle throughput Q \(v/500s\) in the 8U \+6S configuration \(a,b\) and the 4U \+10S configuration \(c, d\) for the entire network. For the 8U \+ 6S configuration, our method consistently outperforms the baseline for all five RV penetration rates, in both W and Q. \(a\): W decreases for 40%, 60% and 80%, while 50% and 70% show higher values. \(b\): Q increases for 40%, 60% and 80%, while 50% and 70% show lower values. For the 4U \+ 10S configuration, our method outperforms the baseline when RV

rate = 80% in W and outperforms the baseline when RV rates are above 40% in Q. \(c\): W decreases for 40%, 50%, 60% and 80%, while 70% shows higher values. \(d\): Q increases for 40%, 50%, 60% and 80%, while 70% shows lower values. 

Fig. 3: Average waiting time W \(s\) for 14 intersections when RV rate = 50% \(upper figure\) and 80% \(lower figure\). Ours is the lowest value among five configurations from 2U \+ 12S to 10U \+ 4S. At the 50% RV rate, intersections 1, 4, 5, 6, 8, 10, 11, 12 and 14 show that the best W is lower than the traffic light control \(TL\). At the 80% RV rate, intersections 1, 2, 3, 4, 5, 6, 8, 10, 11, 12 and 14 show that the best W is lower than TL. These results indicate that our method can reduce vehicle waiting times at most intersections compared to traffic light control. Additionally, the performance of our method tends to improve as the RV rate increases from 50% to 80%. 

ther lowers waiting time to 5.74 s and boosts throughput V. CONCLUSION AND FUTURE WORK

to 477 v/500s. The 10U \+ 4S configuration also shows strong performance with a waiting time of 5.94 s and the We propose the first application of decentralized multi-highest throughput of 483 v/500s. In contrast, the 4U \+ 10S

agent reinforcement learning for large-scale mixed-traffic configuration underperforms in waiting time \(6.9 s\) with a intersection control, where RL-driven RVs regulate some throughput close to baseline \(452 v/500s\), and the 6U \+

intersections while traffic signals control others. Unlike pre-8S delivers moderate gains \(6.43 s and 468 v/500s\). In vious studies focused solely on signalized or unsignalized general, these results suggest that at a 40% RV penetration, control, we explore their coexistence to optimize urban configurations such as 2U \+ 12S, 8U \+ 6S, and 10U \+ 4S

mobility. Our MARL-based approach enables RVs to adapt could reduce delays and improve throughput compared to the dynamically to local traffic conditions, offering a flexible baseline, while the others show mixed performance. 

alternative to static signals. Experiments on a 14-intersection real-world network \(Colorado Springs, CO, USA\) compare five configurations of mixed control against a fully signalized At the 60% RV rate, improvements are more obvious baseline. Traffic performance is evaluated using average with 10U \+ 4S and 8U \+ 6S reducing waiting times to waiting time and vehicle throughput. The results show that 5.51 s and 5.22 s and achieving throughput of 481 v/500s at 80% RV penetration, W decreases by 20% \(from 6.17 s to and 492 v/500s, while 6U \+ 8S and 4U \+ 10S remain near 5.09 s\) while Q increases by 9% \(from 454 to 493 vehicles or slightly above baseline in waiting time. For intersection 6, per 500 seconds\). This research examines the transition from there is an improvement with an 98.82% reduction in W . For conventional traffic signals to autonomous intersection man-the 70%, although 2U \+ 12S and 8U \+ 6S continue to offer agement. With the rise of self-driving technology, our results lower waiting times \(5.9 s and 5.6 s\) and improved through-suggest that integrating autonomous control can enhance put \(471 v/500s and 490 v/500s\), the configurations 4U \+

traffic flow while reducing the need for static signals. By 10S, 6U \+ 8S and 10U \+ 4S get higher W and higher Q

demonstrating these benefits, our study lays the groundwork compared to the baseline 0U \+ 14S. The 6U \+ 8S configura-for future developments in signal-free intersection systems. 

tion again shows degraded waiting times \(7.85 s\) and slightly While our method shows promise in managing large-lower throughput, and 10U \+ 4S’s waiting time increases to scale mixed traffic with combined control strategies, several 6.23 s. For intersection 6, there is an improvement with an limitations remain. The poor performance of the 6U \+

98.24% reduction in W . The detailed results can be found 8S configuration suggests that network geometry, vehicle at https://github.com/cgchrfchscyrh/MixedTrafficControl\_IR

route distribution, and suboptimal intersection selection may

OS/blob/main/Tables.pdf. 

hinder congestion mitigation. To address this, we plan to

explore adaptive intersection selection. We also plan to

\[17\] Greenlight, 

“A

guide

to

types

of

traffic

signals,” 

https:

investigate how different origin-destination demands affect

//www.greenlighttrafficengineering.com/blog/a-guide-to-types-of-

traffic-signals, accessed: 2025-02-25. 

RV-controlled intersections. Finally, our study focuses solely

\[18\] A. Gholamhosseinian and J. Seitz, “A comprehensive survey on on intersections, overlooking other road structures like one-cooperative intersection management for heterogeneous connected way streets and roundabouts. Expanding our analysis to vehicles,” IEEE Access, vol. 10, pp. 7937–7972, 2022. 

\[19\] S. S. S. M. Qadri, M. A. Gökçe, and E. Öner, “State-of-art review of diverse network layouts will enhance the adaptability of our traffic signal control methods: challenges and opportunities,” European method to real-world traffic management. 

transport research review, vol. 12, pp. 1–23, 2020. 

\[20\] K. Dresner and P. Stone, “A multiagent approach to autonomous REFERENCES

intersection management,” Journal of artificial intelligence research, vol. 31, pp. 591–656, 2008. 

\[1\] P. newswire, “Inrix 2024 global traffic scorecard: Employees & 

\[21\] Q. Jin, G. Wu, K. Boriboonsomsin, and M. Barth, “Platoon-based consumers returned to downtowns, traffic delays & costs grew,” 

multi-agent intersection management for connected vehicle,” in 16th

https://www.prnewswire.com/news-releases/inrix-2024-global-traffic-

international ieee conference on intelligent transportation systems \(itsc

scorecard-employees--consumers-returned-to-downtowns-traffic-

2013\). 

IEEE, 2013, pp. 1462–1467. 

delays--costs-grew-302342464.html, accessed: 2025-02-20. 

\[22\] X. Chen, M. Hu, B. Xu, Y. Bian, and H. Qin, “Improved reservation-

\[2\] INRIX, “Inrix 2024 global traffic scorecard: London most con-based method with controllable gap strategy for vehicle coordination gested city in europe; congestion costing the uk £7.7 billion.” 

at non-signalized intersections,” Physica A: Statistical Mechanics and

https://inrix.com/press-releases/2024-global-traffic-scorecard-uk/, acits Applications, vol. 604, p. 127953, 2022. 

cessed: 2025-02-20. 

\[23\] A. Mirheli, M. Tajalli, L. Hajibabai, and A. Hajbabaie, “A consensus-

\[3\] Z. Yan and C. Wu, “Reinforcement learning for mixed autonomy based distributed trajectory control in a signal-free intersection,” 

intersections,” in 2021 IEEE International Intelligent Transportation Transportation research part C: emerging technologies, vol. 100, pp. 

Systems Conference \(ITSC\). 

IEEE, 2021, pp. 2089–2094. 

161–176, 2019. 

\[4\] D. Wang, W. Li, L. Zhu, and J. Pan, “Learning to control and coordi-

\[24\] A. A. Malikopoulos, C. G. Cassandras, and Y. J. Zhang, “A decen-nate mixed traffic through robot vehicles at complex and unsignalized tralized energy-optimal control framework for connected automated intersections,” The International Journal of Robotics Research, p. 

vehicles at signal-free intersections,” Automatica, vol. 93, pp. 244–

02783649241284069, 2024. 

256, 2018. 

\[5\] M. Villarreal, D. Wang, J. Pan, and W. Li, “Analyzing emissions and

\[25\] I. K. Adu, D. K. Boah, and V. Tulasi, “Application of system of linear energy efficiency in mixed traffic control at unsignalized intersections,” 

equations to traffic flow for a network of four one-way streets in in IEEE Forum for Innovative Sustainable Transportation Systems kumasi, ghana,” International Journal of Contemporary Mathematical \(FISTS\), 2024, pp. 1–7. 

Sciences, vol. 9, no. 14, pp. 653–660, 2014. 

\[6\] I. Islam, W. Li, S. Li, and K. Heaslip, “Heterogeneous mixed traffic

\[26\] C. Wu, A. R. Kreidieh, K. Parvate, E. Vinitsky, and A. M. Bayen, control and coordination,” in Heterogeneous Mixed Traffic Control and

“Flow: A modular learning framework for mixed autonomy traffic,” 

Coordination, 2024. 

IEEE Transactions on Robotics, vol. 38, no. 2, pp. 1270–1286, 2021. 

\[7\] M. Villarreal, B. Poudel, J. Pan, and W. Li, “Mixed traffic control and

\[27\] C. You, J. Lu, D. Filev, and P. Tsiotras, “Advanced planning for coordination from pixels,” in 2024 IEEE International Conference on autonomous vehicles using reinforcement learning and deep inverse Robotics and Automation \(ICRA\). 

IEEE, 2024, pp. 4488–4494. 

reinforcement learning,” Robotics and Autonomous Systems, vol. 114, 

\[8\] B. Poudel, W. Li, and S. Li, “Carl: Congestion-aware reinforcement pp. 1–18, 2019. 

learning for imitation-based perturbations in mixed traffic control,” in

\[28\] M. Villarreal, B. Poudel, and W. Li, “Can chatgpt enable its? the case 2024 IEEE 14th International Conference on CYBER Technology in of mixed traffic control via reinforcement learning,” in IEEE Interna-Automation, Control, and Intelligent Systems \(CYBER\). 

IEEE, 2024, 

tional Conference on Intelligent Transportation Systems \(ITSC\), 2023, pp. 7–14. 

pp. 3749–3755. 

\[9\] B. Poudel, W. Li, and K. Heaslip, “Endurl: Enhancing safety, stability, 

\[29\] R. Niroumand, L. Hajibabai, and A. Hajbabaie, “White phase inter-and efficiency of mixed traffic under real-world perturbations via section control through distributed coordination: A mobile controller reinforcement learning,” in 2024 IEEE/RSJ International Conference paradigm in a mixed traffic stream,” IEEE Transactions on Intelligent on Intelligent Robots and Systems \(IROS\). 

IEEE, 2024, pp. 13 671–

Transportation Systems, vol. 24, no. 3, pp. 2993–3007, 2023. 

13 678. 

\[30\] L. Ferrarotti, M. Luca, G. Santin, G. Previati, G. Mastinu, M. Gobbi, 

\[10\] B. Peng, M. F. Keskin, B. Kulcsár, and H. Wymeersch, “Connected au-E. Campi, L. Uccello, A. Albanese, P. Zalaya et al., “Autonomous and tonomous vehicles for improving mixed traffic efficiency in unsignal-human-driven vehicles interacting in a roundabout: a quantitative and ized intersections with deep reinforcement learning,” Communications qualitative evaluation,” IEEE Access, 2024. 

in Transportation Research, vol. 1, p. 100017, 2021. 

\[31\] S.-Y. Xu, X.-M. Chen, Z.-J. Wang, Y.-H. Hu, and X.-T. Han, 

\[11\] Y. Shi, Y. Liu, Y. Qi, and Q. Han, “A control method with reinforce-

“Decision-making models for autonomous vehicles at unsignalized ment learning for urban un-signalized intersection in hybrid traffic intersections based on deep reinforcement learning,” in 2022 Interna-environment,” Sensors, vol. 22, no. 3, p. 779, 2022. 

tional Conference on Advanced Robotics and Mechatronics \(ICARM\). 

\[12\] C. Spatharis and K. Blekas, “Multiagent reinforcement learning for IEEE, 2022, pp. 672–677. 

autonomous driving in traffic zones with unsignalized intersections,” 

\[32\] S. Kai, B. Wang, D. Chen, J. Hao, H. Zhang, and W. Liu, “A Journal of Intelligent Transportation Systems, vol. 28, no. 1, pp. 103–

multi-task reinforcement learning approach for navigating unsignalized 119, 2024. 

intersections,” in 2020 IEEE Intelligent Vehicles Symposium \(IV\). 

\[13\] P. A. Lopez, M. Behrisch, L. Bieker-Walz, J. Erdmann, Y.-P. Flötteröd, IEEE, 2020, pp. 1583–1588. 

R. Hilbrich, L. Lücken, J. Rummel, P. Wagner, and E. Wießner, “Mi-

\[33\] L. Wang, J. Liu, H. Shao, W. Wang, R. Chen, Y. Liu, and S. L. Waslan-croscopic traffic simulation using sumo,” in 2018 21st international der, “Efficient reinforcement learning for autonomous driving with conference on intelligent transportation systems \(ITSC\). 

Ieee, 2018, 

parameterized skills and priors,” arXiv preprint arXiv:2305.04412, pp. 2575–2582. 

2023. 

\[14\] R. Zhang, A. Ishikawa, W. Wang, B. Striner, and O. K. Tonguz, “Using

\[34\] S. Khaitan and J. M. Dolan, “State dropout-based curriculum rein-reinforcement learning with partial vehicle detection for intelligent forcement learning for self-driving at unsignalized intersections,” in traffic signal control,” IEEE Transactions on Intelligent Transportation 2022 IEEE/RSJ International Conference on Intelligent Robots and Systems, vol. 22, no. 1, pp. 404–415, 2020. 

Systems \(IROS\). 

IEEE, 2022, pp. 12 219–12 224. 

\[15\] M. Gregurić, M. Vujić, C. Alexopoulos, and M. Miletić, “Application

\[35\] J. Yin, Z. Jiang, Q. Liang, W. Li, Z. Pan, H. Li, and J. Liu, “Efficient-of deep reinforcement learning in traffic signal control: An overview enhanced reinforcement learning for autonomous driving in urban and impact of open traffic data,” Applied Sciences, vol. 10, no. 11, p. 

traffic scenarios,” in 2023 IEEE 26th International Conference on 4011, 2020. 

Intelligent Transportation Systems \(ITSC\). IEEE, 2023, pp. 887–893. 

\[16\] NACTO, 

“Fixed

vs. 

actuated

signalization,” 

https://nacto.org/

\[36\] D. Wang, W. Li, and J. Pan, “Large-scale mixed traffic control using

publication/urban-street-design-guide/intersection-design-elements/

dynamic vehicle routing and privacy-preserving crowdsourcing,” IEEE

traffic-signals/fixed-vs-actuated-signalization/, accessed: 2025-02-25. 

Internet of Things Journal, vol. 11, no. 2, pp. 1981–1989, 2023. 

\[37\] C. Ma, A. Li, Y. Du, H. Dong, and Y. Yang, “Efficient and scalable reinforcement learning for large-scale network control,” Nature Machine Intelligence, vol. 6, no. 9, pp. 1006–1020, 2024. 

\[38\] M. Treiber, A. Hennecke, and D. Helbing, “Congested traffic states in empirical observations and microscopic simulations,” Physical review E, vol. 62, no. 2, p. 1805, 2000. 

\[39\] M. Hessel, J. Modayil, H. Van Hasselt, T. Schaul, G. Ostrovski, W. Dabney, D. Horgan, B. Piot, M. Azar, and D. Silver, “Rainbow: Combining improvements in deep reinforcement learning,” in Proceed-ings of the AAAI conference on artificial intelligence, vol. 32, no. 1, 2018. 

Intersection control configuration Intersection

0U \+ 14S \(baseline\)

2U \+ 12S

4U \+ 10S

6U \+ 8S

8U \+ 6S

10U \+ 4S

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

1

5.27

391

0.5

326

0.58

337

0.7

338

0.71

347

0.91

339

2

3.07

194

4.99

190

4.95

189

0.27

211

0.35

211

0.34

210

3

7.26

464

7.42

334

7.29

348

7.98

342

7.49

358

6.93

357

4

0.95

56

2.58

64

2.45

62

0.11

66

0.12

65

0.31

70

5

9.74

515

10.33

501

12.8

390

12.52

396

12.17

379

13.08

372

6

5.10

88

3.43

87

4.48

86

4.44

87

0.1

104

0.08

107

7

12.89

488

13.29

490

21.34

373

21.27

378

20.14

378

19.28

375

8

7.62

198

6.66

180

7.36

182

7.15

184

4.22

174

4.15

179

9

1.91

190

2.07

187

2.01

189

2.08

193

2.09

191

2.1

189

10

0.28

39

0.36

44

0.33

42

0.38

42

0.4

43

0.01

46

11

17.83

144

16.21

136

17.22

140

16.4

143

16.56

142

16.89

143

12

0.79

112

0.78

113

0.81

116

0.81

116

1.13

121

0.14

127

13

4.19

221

4.84

226

5.01

229

5.12

232

5.21

235

5.51

236

14

9.49

354

8.07

356

8.45

359

8.4

358

8.53

362

8.35

363

Network

6.17

454

5.89

474

6.9

452

6.43

468

5.74

477

5.94

483

TABLE III: Average waiting time W and vehicle throughput Q for fourteen individual intersections and entire network when RV rate

= 40%. The configurations 2U \+ 12S, 8U \+ 6S and 10U \+ 4S achieve lower network W and higher network Q, while 4U \+ 10S

and 6U \+ 8S get higher W compared to the baseline 0U \+ 14S. For the network, bold values indicate the highest improvement for the two metrics, occurring at 8U \+ 6S and 10U \+ 4S configuration. Our method impacts individual intersections differently: some achieve lower W and others experience higher W . For intersection 6, bold value indicates the highest improvement with an 98.43% reduction in W . 8U \+ 6S achieves the lowest W of 5.74 s across the entire network and 10U \+ 4S has the lowest W at five of the 14 intersections. 

For Q, 10U \+ 4S achieves the highest network-wide value of 483 v/500s and has the highest Q at six intersections, while the baseline ranks second with five intersections. These results indicate that 10U \+ 4S is the best configuration for maximizing throughput. 

Intersection control configuration

Intersection

0U \+ 14S \(baseline\)

2U \+ 12S

4U \+ 10S

6U \+ 8S

8U \+ 6S

10U \+ 4S

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

1

5.27

391

0.6

346

0.64

356

0.82

355

0.88

356

0.85

348

2

3.07

194

4.91

190

4.96

190

2.91

199

0.22

212

0.23

212

3

7.26

464

5.42

372

5.7

397

5.61

400

5.6

396

6.83

371

4

0.95

56

2.57

65

2.51

65

6.67

59

0.11

66

0.45

69

5

9.74

515

9.58

499

9.25

426

9.63

411

9.98

420

11.9

394

6

5.10

88

3.16

87

4.35

86

4.4

87

0.06

101

0.07

107

7

12.89

488

13.36

493

18.19

406

16.46

422

16.31

414

17.31

405

8

7.62

198

6.71

184

7.18

185

7.34

186

2.96

187

4.03

175

9

1.91

190

2.03

191

2.1

188

2.03

190

2.06

190

2.06

190

10

0.28

39

0.37

44

0.37

43

0.39

43

0.4

43

0.01

45

11

17.83

144

15.83

138

16.89

143

16.87

141

17.22

138

17.02

141

12

0.79

112

0.76

115

0.8

115

0.81

117

1.15

120

0.15

127

13

4.19

221

4.91

229

5.04

230

5.01

232

5.21

234

5.57

237

14

9.49

354

8.21

355

8.45

357

8.23

359

8.34

363

8.24

361

Network

6.17

454

5.72

475

6.22

468

6.41

476

5.22

492

5.51

481

TABLE IV: Average waiting time W and vehicle throughput Q for fourteen individual intersections and entire network when RV rate =

60%. The configurations 2U \+12S, 8U \+6S and 10U \+4S achieve lower network W and higher network Q, while 4U \+10S and 6U \+8S

get higher W and higher Q compared to the baseline 0U \+ 14S. For the network, bold values indicate the highest improvement for the two metrics, both occurring at 8U \+ 6S configuration. Our method impacts individual intersections differently: some achieve lower W and others experience higher W . For intersection 6, bold value indicates the highest improvement with an 98.82% reduction in W . 8U \+ 6S

achieves the lowest W of 5.22 s across the entire network and has the lowest W at four of the 14 intersections, making it the best configuration for minimizing delays. For Q, 8U \+ 6S also achieves the highest network-wide value of 492 v/500s and 10U \+ 4S has the highest Q at five intersections. These results indicate that 8U \+ 6S is the best configuration for maximizing network throughput and 10U \+ 4S is the best for maximizing individual intersection throughput. 

Intersection control configuration Intersection

0U \+ 14S \(baseline\)

2U \+ 12S

4U \+ 10S

6U \+ 8S

8U \+ 6S

10U \+ 4S

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

W \(s\)

Q \(v/500s\)

1

5.27

391

0.62

348

0.83

356

0.76

357

0.79

363

0.72

361

2

3.07

194

4.92

190

4.89

191

18.71

165

4.0

198

6.33

193

3

7.26

464

5.34

396

6.38

388

7.75

371

5.54

414

5.91

406

4

0.95

56

2.48

63

2.48

63

7.22

53

0.28

65

5.8

61

5

9.74

515

10.73

487

9.2

421

9.93

420

9.13

432

9.81

409

6

5.10

88

4.5

87

4.41

86

4.46

87

0.09

101

0.11

104

7

12.89

488

13.41

492

19.11

410

19.75

395

17.17

423

18.25

421

8

7.62

198

6.85

181

7.26

186

7.05

185

3.71

182

4.03

175

9

1.91

190

2.04

187

2.05

190

1.99

191

2.05

191

2.02

189

10

0.28

39

0.36

43

0.33

42

0.36

41

0.39

43

0.01

45

11

17.83

144

16.53

139

17.39

139

16.61

141

16.87

141

16.85

140

12

0.79

112

0.78

113

0.81

117

0.81

117

1.15

122

0.16

126

13

4.19

221

4.87

227

4.98

230

5.07

233

5.13

234

5.57

236

14

9.49

354

8.13

359

8.29

358

8.3

358

8.22

361

8.28

360

Network

6.17

454

5.9

471

6.36

457

7.85

453

5.6

490

6.23

487

TABLE V: Average waiting time W and vehicle throughput Q for fourteen individual intersections and entire network when RV rate =

70%. The configurations 2U \+12S and 8U \+6S achieve lower network W and higher network Q, while 4U \+10S, 6U \+8S and 10U \+4S

get higher W and higher Q compared to the baseline 0U \+ 14S. For the network, bold values indicate the highest improvement for the two metrics, both occurring at 8U \+ 6S configuration. Our method impacts individual intersections differently: some achieve lower W and others experience higher W . For intersection 6, bold value indicates the highest improvement with an 98.24% reduction in W . 8U \+ 6S

achieves the lowest W of 5.6 s across the entire network and has the lowest W at four of the 14 intersections, making it the best configuration for minimizing delays. For Q, 8U \+ 6S achieves the highest network-wide value of 490 v/500s and 0U \+ 14S has the highest Q at five intersections. These results indicate that 8U \+ 6S is the best configuration for maximizing network throughput. 


# Document Outline

+ Introduction 
+ Related Work 
+ Methodology  
	+ RL-based Control for Mixed Traffic at Intersections 
	+ Vehicle Behavior Modeling 
	+ Mixed Control of Intersections 
	+ Evaluation Metrics  
		+ Average Waiting Time \(W\) 
		+ Vehicle Throughput \(Q\) 


+ Experiments and Results  
	+ Experiment Set-up 
	+ Overall Results 
	+ Results At Various RV Rates 

+ Conclusion and Future Work 
+ References



