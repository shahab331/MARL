1

A Universal Multi-Vehicle Cooperative Decision-Making Approach in Structured Roads by Mixed-Integer Potential Game

Chengzhen Meng, Zhenmin Huang, and Jun Ma Abstract—Due to the intricate of real-world road topologies These challenges stem from the inherent non-linearity, non-and the inherent complexity of autonomous vehicles, cooperative convexity, and discrete characteristics of cooperative decision-decision-making for multiple connected autonomous vehicles making problems, as well as the varying topological structures \(CAVs\) remains a significant challenge. Currently, most methods associated with different traffic scenarios. To address these are tailored to specific scenarios, and the efficiency of existing optimization and learning methods applicable to diverse scenarios difficulties, a considerable amount of work has been proposed is hindered by the complexity of modeling and data dependency, 

\[8\]–\[10\], primarily divided into two categories: learning-based which limit their real-world applicability. To address these methods and optimization-based methods. 

issues, this paper proposes a universal multi-vehicle cooperative Learning-based methods are known for their wide ap-decision-making method in structured roads with game theory. 

plicability. For instance, in \[11\], a cooperative multi-agent We transform the decision-making problem into a graph path searching problem within a way-point graph framework. The reinforcement learning \(MARL\) algorithm, based on value problem is formulated as a mixed-integer linear programming function decomposition for centralized training and decentral-problem \(MILP\) first and transformed into a mixed-integer ized execution, is proposed. This enables CAVs to quickly potential game \(MIPG\), which reduces the scope of problem and pass through mixed traffic flows in emergency situations. In ensures that no player needs to sacrifice for the overall cost. 

\[12\], a method is introduced for cooperative decision-making Two Gauss-Seidel algorithms for cooperative decision-making are presented to solve the MIPG problem and obtain the in emergencies, based on a deep reinforcement learning \(DRL\) Nash equilibrium solutions. Specifically, the sequential Gauss-model to evaluate potential emergency destinations. It also Seidel algorithm for cooperative decision-making considers the proposes a new representation called the safety evaluation map varying degrees of CAV interactions and flexibility in adjustment \(SEM\) to characterize the evaluation results. In \[13\], \[14\], 

strategies to determine optimization priorities, which reduces the and \[15\], learning-based methods are utilized, such as deep frequency of ineffective optimizations. Experimental evaluations across various urban traffic scenarios with different topological learning and multi-agent reinforcement learning, to enhance structures demonstrate the effectiveness and efficiency of the pro-the operational efficiency and safety of CAVs at intersections. 

posed method compared with MILP and comparisons of different Learning-based approaches can effectively handle complex optimization sequences validate the efficiency of the sequential interactions between CAVs, which are often difficult to model Gauss-Seidel algorithm for cooperative decision-making. 

using traditional methods. However, these methods suffer from Index Terms—Connected autonomous vehicles \(CAVs\), coop-poor interpretability, which is particularly problematic in the erative decision-making, mixed-integer potential game \(MIPG\), safety-critical field of autonomous driving. Moreover, they rely Gauss-Seidel algorithm

heavily on specific data for training across different traffic scenarios. Optimization-based methods, unlike learning-based approaches, offer strong interpretability, which are able to find I. INTRODUCTION

optimal solutions and ensure solution quality. In \[16\], an op-arXiv:2409.16190v1 \[cs.RO\] 24 Sep 2024 IN recent years, the rapid development of autonomous timalcontrolmodelisproposed,whichutilizesapproximately driving technology has marked a series of significant geometric contour models, dynamic externally tangent rect-achievements in this field \[1\]–\[3\], particularly with the emer-angle, and inflated rectangle to describe the platoon’s profile. 

gence of connected autonomous vehicles \(CAVs\), which are The optimal control model also constructs collision avoidance widely regarded as a milestone in the realm of autonomous constraints to ensure safety. However, most methods model driving \[4\]. Through vehicle-to-everything \(V2X\) technology the problem as mixed-integer linear programming problem

\[5\]–\[7\], CAVs can communicate with road infrastructure and \(MILP\) \[17\], \[18\], mixed-integer potential game \(MIQP\) \[19\], 

other vehicles, making the realization of collective intelli-

\[20\], and other NP-hard problems \[21\], leading to a significant gence and cooperative decision-making possible. However, decrease in solving efficiency as the problem size increases. 

cooperative CAV decision-making still faces many challenges. 

In recent years, game theory has been considered an ideal tool for simulating and handling non-cooperative behavior Chengzhen Meng, Zhenmin Huang, and Jun Ma are with the Robotics due to its convenience in modeling the interactions between and Autonomous Systems Thrust, The Hong Kong University of Science CAVs and considering the selfishness of road users. Unlike and Technology, Guangzhou, China, and also the Department of Electronic optimization-based methods, game theory aims to achieve and Computer Engineering, The Hong Kong University of Science and Technology, Hong Kong SAR, China \(e-mail: cmeng403@connect.hkust-results that are more satisfactory to all players \[22\]. A gz.edu.cn; zhuangdf@connect.ust.hk; jun.ma@ust.hk\). 

cooperative decision-making framework based on coalitional



2

game theory is proposed by \[23\] for addressing the multi-lane merging problem of CAVs in merging areas, enhancing safety, comfort, and efficiency. In \[24\], a game-theoretic decision-making framework is designed for CAVs at unsignalized intersection, taking into account both societal and individual inter-ests. In \[25\], a game-theoretic decision-making framework is introduced to solve the merging, passing, and exiting problems of CAVs in unsignalized roundabout areas, considering both individual benefits of single CAV and the social benefits of the entire traffic system. Game theory and optimization methods have strong interpretability but are often modeled for specific Fig. 1. An example of way-point graph. Different arrows represent edges for scenarios, addressing issues on a case-by-case basis, such as different driving purposes, including straight traveling, lane changing, etc. 

multi-lane \[26\], \[27\], intersection \[28\]–\[30\], roundabout \[31\]–

\[33\], etc., which results in weak generalizability. 

II. PROBLEM FORMULATION AS MIXED-INTEGER LINEAR

To address the aforementioned issues in decision-making of PROGRAMMING

CAVs, this paper proposes an optimization method combined In this section, we propose a universal cooperative decision-with game theory. It abstracts structured roads and transforms making model for CAVs that can be applied to various urban them into directed acyclic graphs \(DAGs\) to convert the coop-traffic scenarios with structured roads. By discretizing the erative decision-making problem into a path-finding problem. 

road network and transforming it into a DAG, the cooper-This is then approximately modeled as an MIPG problem ative decision-making problem is transformed into a graph using game theory, and two algorithms are proposed to solve path searching problem, decoupling the relationship between this problem efficiently while ensuring safety and efficiency problem formulation and road structure. With the binary in driving. The main contributions of this paper are fourfold: decision-making variables and linear constraints, the problem \(1\) The CAVs cooperative decision-making problem is is formulated as an MILP problem. Lane-selection decisions transformed into a graph path searching problem within a are reflected in the paths on the graph. 

way-point graph framework. We first model the graph path searching problem as an MILP and transform it into an MIPG

problem with game theory. The transformation reduces the A. Way-Point Graph

problem from solving for all CAVs at once to solving for In this section, we introduce the concept of the way-point each CAV individually in succession, which maintains a rather graph in \[34\]. For urban traffic scenarios with structured small scope of the problem while ensuring that no player needs roads, we create waypoints by sampling equidistantly along to sacrifice for the overall cost. 

the centerline of the road and constructing paths between each \(2\) A Gauss-Seidel algorithm for cooperative decision-waypoint based on reachability. The resulting way-point graph making is proposed for solving the MIPG problem, which is essentially a DAG. With the introduction of the way-point optimizes the decision variables of each CAV separately during graph, we can view the decision-making process of CAVs as the iteration process rather than considering all of them collec-moving along paths in the graph from the starting point to tively. Therefore, the Gauss-Seidel algorithm for cooperative the desired destination. This approach transforms the decision-decision-making leads to a high solving efficiency compared making process of CAVs into a path searching problem in a to MILP methods. 

DAG. Since the construction of the way-point graph is related \(3\) On the basis of the Gauss-Seidel algorithm for cooper-only to the road structure and not affected by the problem’s ative decision-making, a sequential Gauss-Seidel algorithm is modeling and optimization process, the way-point graph can further proposed that considers multiple initial factors to de-be pre-constructed. 

termine optimization priorities, and this significantly improves One key issue is that the starting position of the CAV does the efficiency of algorithmic solutions. 

not completely overlap with the waypoints on the way-point \(4\) The feasibility of the proposed algorithms is verified in graph, making it impossible to determine the starting point three different common structured urban traffic scenarios. The of the CAV on the graph. This problem can be solved by results showcase the generalization and validate the efficiency extending the original way-point graph. For each CAV, its of the proposed method. 

starting point is added as a new node to the way-point graph, This paper is structured as follows: Section II introduces the and this node is connected to the closest fixed number of edges problem modeling process, setting constraints, and describing in front of the CAV. An example of this extension is shown the problem as an MILP problem. Section III elaborates on in Fig. 1. 

modeling the problem as an MIPG problem by combining it We define the extended way-point graph as G = \(V, E \), with game theory, and presents the conditions for equilibrium where V is the set of vertices and E is the sets of edges. Be-solutions. Section IV proposes two algorithms for efficiently cause of the differences between the starting position of CAVs, solving the equilibrium problem. Section V verifies the effec-which is denoted as the set N , a sub-graph Gi = \(Vi, Ei\) is tiveness of the proposed methods in three common structured defined for a particular CAV i, i ∈ N . We use v1 −→ v2 to urban traffic scenarios. Finally, we summarize the conclusion denote if there exists a path from v1 ∈ V to v2 ∈ V. Suppose and future work in Section VI. 

that for CAV i, its starting point can be denoted as si ∈ V, and

3

the set of possible destination can be denoted as desi ⊂ V, Destination Constraints

then we present the following definitions: X

X

P e = 1, ∀i ∈ N . 

i

\(6\)

Definition 1. For vertex i, we define its forward reachable set v∈desi e∈Ev,in

i

F \(v\) as:

Continuity Constraints

X

X

F \(v\) = \{v1 | v ∈ V, v −→ v1\} , v /

∈ desi

\(1\)

P e =

P e, ∀i ∈ N , ∀v ∈ ˜

V

i

i

i

\(7\)

e∈Ev,in

e∈Ev,out

i

and its backward set B \(v\):

i

where ˜

Vi = \{v | v ∈ Vi, v ̸= si, v /

∈ desi\}. 

B \(v\) = \{v1 | v ∈ V, v1 −→ v\} , v ̸= si. 

\(2\)

Velocity Constraints: To meet the requirements for comfort and to avoid safety issues caused by large velocity fluctuations, In most urban road traffic scenarios, reversing is not per-CAVs should maintain a stable velocity as much as possible. 

mitted. Therefore, for a specific CAV i, its subgraph should Therefore, we set a reference velocity V r for each CAV. For i

only include a set of reachable vertices that can reach at least the edge e that CAV i passes through, we define the velocity one destination vertex, as well as a set of edges composed of deviation as ∆V e = V e−V r, where V e is the average velocity i

i

i

i

these vertices. With the above definitions, the sets of vertices of the CAV i on edge e. To reflect the velocity deviation of i and edges can be expressed as follows: on edge e in the time domain \[te1 , te2 \], where e i

i

1 and e2 are the

V

starting point and ending point of edge e, we aim to minimize i = F \(si\) ∩ \(S

B \(v\)\), 

v∈desi

\(3\)

|△V e \(te2 − te1 \)| and the constraints can be expressed as: E

i

i

i

i = \{e | e ∈ E , ve

∈ V

∈ V

1

i, ve2

i\}

le − V r \(te2 − te1 \) ≤ M \(1 − P e\) \+ se i

i

i

i

i

where e1 and e2 are the starting point and ending point of le − V r \(te2 − te1 \) ≥ −M \(1 − P e\) − se i

\(8\)

i

i

i

i

edge e. An important binary decision variable is introduced as

∀i ∈ N , ∀e ∈ E

following:

i

where le is the length of edge e, and M is a large constant used \(1 if i passes through e, 

in the big-M method \[35\]. \[se, se\] is a pair of slack variables P e =

∀i ∈ N , ∀e ∈ E

i

i

i

i. 

0

if i does not pass through e, 

to penalize the changes of velocity. To ensure that the average \(4\)

velocity V e is bounded, which means V min ≤ V e ≤ V max, i

i

i

i

Consequently, all edges traversed by CAV i from the starting

\[sei, se\] need to satisfy the following constraints: i

point to the destination can be represented by P e. Additionally, i

0 ≤ se ≤ \(V max − V r\) \(te2 − te1 \) \+ M \(1 − P e\) i

i

i

i

i

i

to determine the time required for CAV i to pass through all 0 ≤ se ≤ V r − V min \(te2 − te1 \) \+ M \(1 − P e\) \(9\)

vertices, we define tv as the time for CAV i to reach vertex v. 

i

i

i

i

i

i

i

It is important to note that if the CAV does not traverse vertex

∀i ∈ N , ∀e ∈ Ei

v, the corresponding tv is considered redundant. 

i

where V max and V min represent the upper and lower bounds i

i

of the velocity of CAV i. 

Longitudinal Acceleration Constraints: To enhance pas-B. Constraints

senger comfort and avoid excessive longitudinal acceleration, 1\) Travel Constraints: For each CAV i, it is essential that it it is essential to constrain the acceleration. We consider the ensures passengers’ safety while navigating the road, ensuring acceleration at vertices by representing it through the velocities both efficiency and comfort. To achieve these objectives, of the edges before and after each vertex. By linearizing this constraints must be imposed on path selection, velocity, lon-approximation, we establish the necessary constraints. The gitudinal acceleration, and steering. Additionally, appropriate detailed derivation process can be found in \[34\]. Here, we cost functions need to be designed to penalize inefficient and present only the final results. 



high-risk behaviors. In this context, we refer to the constraint We divide the interval V min, V max

into k regions and

i

i

design outlined in \[34\], as follows: set a reference velocity V r for each region. Let yαβ be a i,k

i,k

Path Constraints: Our goal is to ensure that for each CAV, binary variable which is 1 if the velocity belongs to a certain the paths from the starting point to the destination points are region \[V min, V max\], and 0 otherwise. The constraints can be i,k

i,k

continuous and uninterrupted. Due to the fact that each CAV

expressed as follows:

can only travel on one edge at a time, effective paths must not have branches. To define path constraints, we introduce X yv,αβ = 1, 

i,k

Ev,out and Ev,in, where Ev,out represents the set of outgoing i

i

i

k

edges from a specific vertex v, and E v,in represents the set of



\! 

i

X

lα \+ lβ





incoming edges to a specific vertex v. Therefore, to ensure yv,αβ

≥ tβ2 − tα1 − M 2 − P α − P β , 

i,k

V min

i

i

i

i

the feasibility of the generated paths, the path constraints are k

i,k

defined as follows:



\! 

X

lα \+ lβ





Starting Point Constraints

yv,αβ

≤ tβ2 − tα1 \+ M 2 − P α − P β , 

i,k

V max

i

i

i

i

k

i,k

X

P e = 1, ∀i ∈ N . 

i

\(5\)

∀i ∈ N , ∀v ∈ ˇ

Vi, α ∈ Ev,in, β ∈ Ev,out. 

i

i

s

\(10\)

e∈E i,out

i

4

h

i

h

i

With the slack variables

γv,αβ, γv,αβ

to penalize the

time span

tα1 , tβ2

represents the time between the two

i,k

i,k

i

i

longitudinal acceleration, the constraints are introduced as: edges α and β, which are the incoming and outgoing edges, respectively, passing through a vertex v. We define the angle tα1 − tv

tβ2 − tv





i

i − i

i ≤ M 3 − P α − P β − yv,αβ \+ γv,αβ, between the two edges α and β as θαβ. The constraints can lα

lβ

i

i

i,k

i,k

be expressed as:

tα1 − tv

tβ2 − tv





i

i − i

i ≤ −M 3 − P α − P β − yv,αβ −γv,αβ, lα

lβ

i

i

i,k

i,k





γ

V r θαβ − M 3 − P α − P β − yv,αβ

≤ ηv,αβ, 

max

tβ2 − tα1

i

i





i,k

i

i

i,k

i,k

γv,αβ ≤

\+ M 3 − P α − P β − yv,αβ , 

i,k

i





2

i

i,k

2 V r

0 ≤ ηv,αβ ≤ ηmax tβ2 − tα1 \+ M 3 − P α − P β − yv,αβ , i

i

i

i

i,k

i,k

i,k





∀i ∈ N , ∀v ∈ ˇ

V

, β ∈ E v,out

γ

i, α ∈ E v,in

i

i

min

tβ2 − tα1

i

i





\(14\)

γv,αβ ≤ −

\+ M 3 − P α − P β − yv,αβ , 

i,k

i



2

i

i,k

where ηv,αβ is the slack variable to be penalized in the 2 V r

i,k

i,k

cost, and ηmax is a pre-defined constant to bound the lateral γv,αβ, γv,αβ ≥ 0, 

acceleration and avoid high-speed turns. For the starting point, i,k

i,k

the constraints can be expressed as:

∀i ∈ N , ∀v ∈ ˇ

Vi, α ∈ Ev,in, β ∈ Ev,out

i

i

\(11\)





V r θinitβ − M 2 − P β − ysi,β

≤ ηsi,β, 

i,k

i

i,k

i,k

where γmin and γmax are constants, denoting the minimum \(15\)

and maximum of deceleration and acceleration, respectively. 

0 ≤ ηsi,β ≤ η

\+ M 2 − P β − ysi,β , 

i,k

maxtβ2

i

i

i,k

For the starting point, the constraints are adjusted accord-

∀i ∈ N , β ∈ Esi,out

i

ingly due to the lack of incoming edges. We denotes V ini i

as the initial velocity of CAV i, then the constraints can be where θinitβ is the angle between the initial heading of CAV

expressed as:

i and edge β. 

X ysi,β = 1, 

2\) Time Constraints: In urban road scenarios, reversing i,k

while driving is generally not permissible. Consequently, the k



\! 

time at points closer to the CAV in the direction of travel must X

lβ





ysi,β

≥ tβ2 − M 1 − P β , 

be less than the time at points farther away. To standardize the i,k

V min

i

i

k

i,k

\(12\)

initial time of all CAVs, we set the initial time for any CAV i



\! 

to be 0, and ensure that the time at all points is non-negative. 

X

lβ





ysi,β

≤ tβ2 \+ M 1 − P β , 

i,k

V max

i

i

These constraints can be expressed as: k

i,k

∀i ∈ N , β ∈ Esi,out. 

tsi = 0, 

i

i

te1 < te2 , ∀i ∈ N , ∀e ∈ E , 

\(16\)

i

i

2V r − V ini

i,k

i

tβ2





tv ≥ 0. 

− i

≤ M 2 − P β − ysi,β \+ γsi,β, 

i



2

lβ

i

i,k

i,k

V r

i,k

3\) Collision Avoidance Constraints: For the purpose of pre-2V r − V ini

venting any potential collision accidents and ensuring driving i,k

i

tβ2





− i

≥ −M 2 − P β − ysi,β − γsi,β, 



2

lβ

i

i,k

i,k

safety, constraints are imposed on CAV i and its surrounding V r

i,k

CAV j. Different from the method in \[34\], in this section, we γ

design collision avoidance constraints for individual CAV as maxtβ2





0 ≤ γsi,β ≤

i

\+ M 2 − P β − ysi,β , 

i,k

the basis for optimizing each CAV in the subsequent algorithm. 



2

i

i,k

2 V r

Here, we assume that the trajectories of other CAVs j are i,k

known when considering collision constraints for CAV i. To γmintβ2





0 ≤ γsi,β ≤ −

i

\+ M 2 − P β − ysi,β , 

avoid collisions, we first introduce the concept of crucial edge i,k



2

i

i,k

eiej

2 V r

pairs \{\(i, ei\) , \(j, ej\)\}, and crucial areas C

as in \[34\]. For

i,k

ij

CAV i and ei ∈ Ei, we define the set of surrounding CAVs as

∀i ∈ N , β ∈ Ev,out. 

i

Ni and consider the situation where the front of i is parallel to \(13\)

e. The volume occupied by CAV i when it is aligned with ei Steering Constraints: To avoid frequent lane changes or is defined as Sei \(θ\) and its location is at \(1 − θ\) pe1 \+ θpe2 , high-speed turns, it is imperative to impose constraints on i

i

i

where pe1 and pe2 represent the locations of starting point steering. In most cases, CAVs generate lateral acceleration i

i

and end point, respectively. Based on this, we introduce the when turning. Therefore, we constrain the lateral acceleration following definitions:

alat. To properly reflect the impact of steering on driving, i

we choose to penalize the integral of lateral acceleration, Definition 2. For i ∈ N ,j ∈ Ni, ei ∈ Ei, and ej ∈ Ej, which corresponds to steering angle and speed. Since steering

\{\(i, ei\) , \(j, ej\)\} forms a crucial edge pair if Se ∩ Se ̸= 0. 

i

j

only occurs at vertices in our proposed method, the integral The set of all the crucial edge pairs is defined as R. 

5

e

Based on this, the crucial area C iej can be defined as: For Case 1.1 and Case 1.2, the positional relationship ij

e

e

between CAV i and CAV j is illustrated in Fig. 2\(a\)-\(b\). 

θ iej = min Sei \(θ\) ∩ S j ̸= 0 , 

ij,1

i

j

0≤θ≤1

Since the movement of CAVs is represented using the positions e

e

θ iej = max Sei \(θ\) ∩ S j ̸= 0 , 

of their center points, this safe distance is equivalent to the ij,2

i

j

\(17\)

0≤θ≤1

previously mentioned Dij. 

e

e

e

e

C iej = \(1 − θ\) pe1 \+ θpe2 | θ iej ≤ θ ≤ θ iej When CAV j moves to the equivalent edge positions ˆ

s iej

ij

i

i

ij,1

ij,2

ij,1

eiej

e

e

and ˆ

s

of the crucial area, we define the limit positions where θ iej and θ iej represent the boundary position of the ij,2

ij,1

ij,2

for CAV i as si,1 and si,2, as shown in Fig. 2, and the crucial area. 

s

s

corresponding times for these positions as t i,1 and t i,2 . For Obviously, the crucial area can be determined before the i

i

s

s

all cases, the method to calculate t i,1 and t i,2 is the same optimization process. Assuming that the motion of CAVs along i

i

and can be expressed as:

a road edge can be approximated as uniform motion, the time tei at position pei can be obtained through linear interpolation: e

e

i,θ

θ

tsi,1 = \(1 − s

i,1 \+ s

i,2 , 

i

i,1\) ti

i,1ti

\(21\)

e

e

e

e

i,1

i,2

tei ≈ \(1 − θ\) t i,1 \+ θt i,2 . 

\(18\)

tsi,2 = \(1 − s

\+ s

. 

i

i,2\) ti

i,2ti

i,θ

i

i

For CAV j, we define the time it enters the crucial area as For Case 1.1, the limit positions can be expressed as: e

e

t iej and the time it exits as t iej . With \(18\), the time CAV j e

ij,1

ij,2

ˆ

s iej \+ Dij

enters the crucial area can be expressed as: ij,1

si,1 =

, 

lei

e

e

e

e

e

\(22\)

t iej ≈ 1 − θ iej t j,1 \+ θ iej t j,2 , eiej

ij,1

ij,1

j

ij,1

j

ˆ

s

\+ D

ij,2

ij

e

e

e

e

e

\(19\)

si,2 =

. 

t iej ≈ 1 − θ iej t j,1 \+ θ iej t j,2 . 

lei

ij,2

ij,2

j

ij,2

j

Due to the different scenarios in which crucial edge pairs A sufficient condition for avoiding collision, as shown in Fig. 

and crucial areas can occur, to reflect generality and obtain

2\(a\), can be expressed as: conditions to avoid collisions in all scenarios, we project the s

e

t i,1 ≤ t iej \+ M 1 − δei , 

movements of CAV j ∈ N

i

ij,1

ij

i onto the direction of motion of

s

\(23\)

i,2

eiej



CAV i, thereby reducing the original two-dimensional motion t

≤ t

\+ M 1 − δei . 

i

ij,2

ij

to one dimension. At the same time, the distance between these For Case 1.2, similarly, it can be expressed as: two CAVs should be greater than the equivalent safe distance. 

For the crucial edge pair \{\(i, e

eiej

i\) , \(j, ej \)\}, we project \(j, ej \)

ˆ

s

− D

ij,1

ij

onto the corresponding \(i, e

si,1 =

, 

i\), where the projected starting

lei

e

and ending points of the crucial area are denoted as ˆ

s iej

e

\(24\)

i ej

ij,1

ˆ

s

− Dij

e

ij,2

and ˆ

s iej . L

si,2 =

. 

ij,2

i and ˆ

Lj are defined as the length of CAV i and lei

the projected length of CAV j on the trajectory of CAV i, respectively. The equivalent safe distance can be expressed as A sufficient condition for avoiding collision, as shown in Fig. 





2\(b\), can be expressed as: Dij = 1 L

. To cover all scenarios, we discuss four 2

i \+ ˆ

Lj

different cases:

s

e

t i,1 ≥ t iej − M δei , 

i

ij,1

ij

\(25\)

• Case 1.1: The angle between e

si,2

eiej

i and ej is less than 90◦

t

≥ t

− M δei . 

i

ij,2

ij

and CAV i passes the crucial area in front of CAV j. 

• Case 1.2: The angle between e

For Case 2.1 and Case 2.2, the position relationship between i and ej is less than 90◦

and CAV i passes the crucial area behind CAV j. 

CAV i and CAV j is as shown in the Fig. 2\(c\)-\(d\). For Case

• Case 2.1: The angle between e

2.1, it is a little different from Case 1.1 and Case 1.2. In i and ej is greater than or

equal to 90◦ CAV i passes the crucial area in front of this condition, we just need to take one limit position into CAV j. 

consideration, which can be expressed as:

• Case 2.2: The angle between ei and ej is greater than or e

ˆ

s iej \+ D

equal to 90◦ CAV i passes the crucial area behind CAV

ij,1

ij

si,2 =

. 

\(26\)

j. 

lei

Based on the above definitions and transformations, we A sufficient condition for avoiding collision in the correspond-derive the condition to avoid collisions: during the process of ing condition, as shown in Fig. 2\(c\), can be expressed as: e

e

CAV j passing through ˆ

s iej to ˆ

s iej , CAV i must always be

ij,1

ij,2

si,2

eiej



either ahead of or behind CAV j. To fully cover all cases for t

≤ t

\+ M 1 − δei . 

\(27\)

i

ij,1

ij

setting the constraints, we introduce a new binary variable δei ij

Similarly, for Case 2.2, as shown in Fig. 2\(d\), the constraints to describe the relative positional relationship between CAV i can be expressed as:

and CAV j:

e

ˆ

s iej \+ D

ij,2

ij

s

, 

\(

i,1 =

1

if i in front of j, 

lei

\(28\)

δei =

∀i ∈ N , ∀e

si,1

eiej

ij

i ∈ R. 

\(20\)

t

≥ t

− M δei . 

0

if i behind j, 

i

ij,2

ij





6

acceleration changes, and turning effects to adapt to the requirements of complex traffic situations and improve operational efficiency and passenger comfort. 

For CAV i, the part of the objective function related to arrival time can be represented as:

X

fi,t =

tv. 

\(31\)

\(a\) Case 1.1

\(b\) Case 1.2

i

v∈desi

The part of the objective function related to velocity changes can be represented as:

X

fi,V =

\(se \+ se\) . 

i

i

\(32\)

e∈Ei

With the term fi,V as a penalty term, the velocity deviation \(c\) Case 2.1

\(d\) Case 2.2

of CAV i is penalized, leading to the velocity of CAV i tracking the reference velocity. The part of the objective Fig. 2. Projection of each point and the relationship of CAV i and CAV j positions. 

function related to longitudinal acceleration can be represented as:

X

X

X

X



2 

Gathering all the cases we discussed above, the constraints fi,a =

V r

γαβ,k \+ γαβ,k

i,k

i,v

i,v

can be expressed as:

v∈ ˜

V

k∈K

i α∈E v,in β∈E v,out

i

i





e

\! 

e

X

X

2 

ˆ

s iej − D

ˆ

s iej − D

\+

V r

γβ,k \+ γβ,k . 

ij,1

ij

e

ij,1

ij e

e

e

i,k

i,s

1 −

t i,1 \+

t i,2 ≥ 1 − θ iej t j,1

i

i,si

le

i

i

ij,1

j

k∈K

i

lei

β∈Ev,out

si

\(33\)

e

e

\+ θ iej t j,2 − M δei , 

ij,1

j

ij

With the part fi,a as a penalty term, the velocity changes e

\! 

e

ˆ

s iej − D

ˆ

s iej − D

of CAV i are constrained, leading to the improvement of ij,2

ij

e

ij,2

ij e

e

e

1 −

t i,1 \+

t i,2 ≥ 1 − θ iej t j,1

le

i

i

ij,2

j

passengers comfort. The part of the objective function related i

lei

to steering can be represented as:

e

e

\+ θ iej t j,2 − M δei , 

ij,2

j

ij

X

X

X

X



e

\! 

e

f

ηαβ,k

ˆ

s iej \+ D

ˆ

s iej \+ D

i,θ =

i,v

ij,1

ij

e

ij,1

ij e

e

e

1 −

t i,1 \+

t i,2 ≤ 1 − θ iej t j,1

v∈ ˜

V

k∈K

i α∈E v,in β∈E v,out

le

i

i

ij,1

j

i

i

i

lei

\(34\)

X

X

e

e

\+

ηβ,k. 

\+ θ iej t j,2 \+ M 1 − δei , 

i,si

ij,1

j

ij

β∈Ev,out k∈K

s



e

\! 

e

i

ˆ

s iej \+ D

ˆ

s iej \+ D

ij,2

ij

e

ij,2

ij e

e

e

1 −

t i,1 \+

t i,2 ≤ 1 − θ iej t j,1

With the part fi,θ as a penalty term, lateral accelerations le

i

i

ij,2

j

i

lei

induced by steering are penalized, leading to the generated e

e

\+ θ iej t j,2 \+ M 1 − δei , 

paths without unnecessary lane changes and abrupt turns. In ij,2

j

ij

∀i, j ∈ N , Angle \(e

conclusion, with all the penalty terms, for each CAV i, the i, ej \) ≤ 90◦. 

\(29\)

objective function can be represented as: Ji = αtfi,t \+ αV fi,V \+ αafi,a \+ αθfi,θ

\(35\)



e

\! 

e

ˆ

s iej \+ D

ˆ

s iej \+ D

ij,1

ij

e

ij,1

ij e

e

e

1 −

t i,1 \+

t i,2 ≥ 1 − θ iej t j,1 where α

le

i

i

ij,2

j

t, αV , αa, and αθ are the weight parameters of each i

lei

objective function part. With the constraints, the decision-e

e

\+ θ iej t j,2 − M δei , 

ij,2

j

ij

making model of each CAV i can be defined as: e

\! 

e

ˆ

s iej \+ D

ˆ

s iej \+ D

ij,2

ij

e

ij,2

ij e

e

e

min

α

1 −

t i,1 \+

t i,2 ≤ 1 − θ iej t j,1

tfi,t \+ αV fi,V \+ αafi,a \+ αθ fi,θ

\(36\)

le

i

i

ij,1

j

i

lei

s.t. 

\(5\) − \(15\), \(29\) − \(30\). 

e

e

\+ θ iej t j,2 \+ M 1 − δei , 

ij,1

j

ij

We introduce c as the number of constraints and n as the

∀i, j ∈ N , Angle \(ei, ej\) ≥ 90◦. 

number of all the CAVs variables. For xi, which we define \(30\)

as xi = \[ti,v, se, ...., ηαβ,k\]T

i

, it contains all the variables of

i,v

Note that Angle \(ei, ej\) denotes the angle between ei and ej. 

CAV i. With the variables of the surrounding CAVs, we define The collision avoidance constraints are linear constraints with x = \(x

n

i, x−i\) ∈ R

as the vector of all the decision variables e

e

respect to t i,1 and t i,2 . 

i

i

in the neighborhood Ni, where x−i represents the variables of surrounding CAVs. Finally, we transform the \(36\) into a C. MILP Formulation

compact form:

min

J

The objective function should account for important indi-i \(xi\)

xi

\(37\)

cators such as arrival time, velocity changes during travel, s.t. 

Ax ≤ b

7

for some suitable A ∈

c×n

n

Algorithm

1

R

and b ∈ R . For i ∈ N , we

Gauss-Seidel

Algorithm

for

Cooperative

define X = \[x

Decision-Making

1, x2, ..., xN \]T . Due to objective function and all of the constraints are linear, the decision-making model is 1: Choose an initial state x \(0\) ∈ X , set k = 0, sign = 0

a standard MILP problem. 

2: while sign ̸= 1 do

3:

for i = 1 to N do

III. MIXED-INTEGER POTENTIAL GAME FORMULATION

4:

Solve the MILP problem of \(37\) with x \(k\) and get a solution of ˇ

x

In principle, by calculating the optimal solution for \(37\), we i \(x−i \(k\)\)

5:

△J

can obtain the decision variables for each CAV and the refer-i \(k\) = Ji \(xi \(k\)\) − Ji \( ˇ

xi \(k\)\)

\( ˇx

ence times of passing through each node, thereby determining i \(k\) , 

if △Ji ≥ ε

6:

xi \(k \+ 1\) =

the paths and time profiles of each CAV. For the decision-xi \(k\) , 

else

making model \(37\), for each CAV, solving the decision-making 7:

x \(k \+ 1\) = \(xi \(k \+ 1\) , x−i \(k\)\)

model independently yields the optimal decision for each 8:

end for

CAV. However, the collision constraints between CAVs are 9:

if x \(k \+ 1\) = x \(k\) then

coupled, and independent solutions cannot guarantee that all 10:

sign = 1

collision constraints are satisfied. Moreover, the cooperative 11:

end if

solution is NP-hard \[36\] with a large problem scope. As the 12:

k = k \+ 1

number of CAVs increases, the computational time for the 13: end while

optimal solution increases exponentially, making it impractical for real-time applications. Therefore, to tackle the problem of computational time growing exponentially as the scale of the iterative process. xi \(k\) and x−i \(k\) , k ∈ N represent vectors problem and to ensure the safety of the decision strategy, we of decision variables of the CAV i and its surrounding CAVs in transform the MILP problem into an MIPG. 

the k-th iteration, respectively. we introduce the cost variation For each CAV, we define the feasible sets X

△J

i \(x−i\)

=

i \(k\) at one iteration:

\{x

ni

n

i ∈ R

| A \(xi, x−i\) ≤ b\} and X = \{x ∈ R | Ax ≤ b\}. 

△Ji \(k\) = Ji \(xi \(k\)\) − Ji \(ˇ

xi \(k\)\)

\(41\)

Moreover, we introduce a function P : n

R

→ R, which we

define as P \(x\) = P

J

where ˇ

x

\(k\). 

i∈N

i \(xi\). For all i ∈ N , and for all

i \(x−i \(k\)\) ∈ x∗

i

xi, yi ∈ Xi \(x−i\), \(38\) holds true. 

P \(x

A. Gauss-Seidel Algorithm for MIPG

i, x−i\) − P \(yi, x−i\) = Ji \(xi\) − Ji \(yi\) . 

\(38\)

We first propose a Gauss-Seidel algorithm for cooperative By \[37\], P is an exact potential function for the proposed decision-making . This algorithm solves an optimization prob-problem. Given the strategies x−i of surrounding CAVs for lem in each iteration process, i.e., solves the optimization CAV i, the best strategies of CAV i is: problem for a specific CAV separately, obtains the optimal argmin

Ji \(xi\)

decision variables ˇ

xi for the CAV in the current situation, and xi

\(39\)

compares them with the original decision to get the decrease s.t. 

\(xi, x−i\) ∈ X . 

in cost. If the decrease in cost is smaller than ε, the original Then we define the notion of equilibrium solution. 

decision xi \(k\) is retained; otherwise, the optimal decision ˇ

xi \(k\) is adopted. To sum up, the Gauss-Seidel algorithm for Definition 3. If there exists a positive real number ε and x∗ ∈

cooperative decision-making is outlined in Algorithm 1. 

X such that

To demonstrate that the decision vector computed by al-J

gorithm is feasible, namely, x∗ ∈ X of the MIPG, we first i \(x∗\) ≤

J

i

inf

i \(xi\) \+ ε

\(40\)

x

suppose \(x

i ∈Xi \(x∗ \)

i \(k\) , x−i \(k\)\) is feasible, i.e., \(xi \(k\) , x−i \(k\)\) ∈

−i

X . The claim of \(xi \(k \+ 1\) , x−i \(k\)\) is true if the original holds for all i ∈ N . We called x∗ ∈ X is an ε-Mixed-Integer decision is retained, i.e., xi \(k \+ 1\) = xi \(k\). On the other Nash Equilibrium \(ε-MINE\) of the game in \(39\). 

hand, if the decision of CAV i changes, i.e., xi \(k \+ 1\) ∈

All x∗ constitute the ε-approximate minimal set. With the ˇ

xi \(x−i \(k\)\), we obtain that xi \(k \+ 1\) ∈ Xi \(x−i \(k\)\) and above definition, the ε-approximate minimal set on X is a \(xi \(k \+ 1\) , \(x−i \(k\)\) ∈ X . Notice that x \(0\) ∈ X , the subset of the ε-MINE strategy \[38\], which means for the ε-decision vector computed by the algorithm is feasible. 

approximate minimal value set x ∈ X , any x∗ ∈ X such that P \(x∗\) ≤ P \(x\) \+ ε is an ε-MINE of the game. Informally, B. Sequential Gauss-Seidel Algorithm for MIPG

an ε-MINE is a set of driving strategies that are almost When multiple CAVs travel in the same direction on the individually optimal, given the safety constraints. 

single lane, certain general cases present no collision risk. 

For instance, there is no collision risk when the rear CAV’s IV. GAUSS-SEIDEL ALGORITHM FOR DECISION-MAKING

velocity is significantly slower than the front CAV’s velocity or As is well known, solving MIPG is a challenging task, due when the rear CAV’s velocity matches the front CAV’s velocity to integer variables involved. Here, we propose algorithms but with consistently lower longitudinal acceleration. In these to compute the ε-MINE for the game problem through an scenarios, there is no necessity for the rear CAV to change





8

optimization. 

Firstly, we introduce the definition of the optimization priority for the CAVs. For CAV i, its optimization sequence Oi is obtained by the function of the reference factors w and the corresponding weights β, i.e., Oi = f \(w, β\), where w = \[w1, w2, ..., wm\]T and β = \[β1, β2, ..., βm\]T . In this problem, the main reference factors are the initial position px,ini, py,ini

and initial velocity V ini. The initial position i

i

i

\(a\) An example of an unsolvable situation. The decision variables of black reflects the complexity of the CAV interactions. When CAVs and blue CAV are fixed while optimizing for the white CAV. The white CAV

are positioned further back in the direction of travel, there can not overtake the front CAVs because both roads are congested and it cannot change the decision variables of the front CAVs in its own iteration. 

are more important edge pairs and interactions become more The collision is occurred. 

complex. When prioritizing the optimization of CAVs with complex interactions before handling other CAVs, changes in the other CAVs can easily cause the initial CAV’s decision to change again, while the decisions of other CAVs with simpler interactions are less likely to change significantly due to collision constraints. Additionally, optimizing decisions for CAVs with complex interactions requires more time. Therefore, CAVs located closer to the front should be optimized first to avoid repetitive processing of CAVs with complex \(b\) An example of a different optimization sequence. By optimizing the interactions. The initial velocity reflects the flexibility of the blue CAV first, the blue CAV chooses to change lanes to overtake the black CAV’s adjustment strategy. The CAVs with slower velocity CAV to avoid collision with the white CAV, which allows the white CAV to take more time to change lane, making it difficult to perform continue straight without collision. Thus, the problem becomes solvable. 

rapid yielding and overtaking maneuvers. Therefore, the opti-Fig. 3. Examples of different optimization sequence. 

mization sequence should prioritize CAVs with slower initial speeds so that the strategies of other CAVs can be based on the strategies of the slower CAVs. We propose some methods to lanes or overtake. Due to the relatively low collision risk in obtain the optimization sequence by considering both factors. 

these situations, they are not our primary concern. To ensure 1\) Linearized Optimization Order Determination Method: the algorithm’s applicability in all situations, we focus on the In the linearized optimization order determination \(LOD\) special case where the rear CAV’s velocity is substantially method, we define the final ranking as the ranking of the higher than the front CAV’s velocity. 

linearly superimposed value of the initial position ranking and In Algorithm 1, optimization is performed sequentially the initial velocity ranking, which can be expressed as: based on the order of the CAVs’ positions in the direction of travel, starting from CAVs with an initial position at Order = Sort βpSortp pini \+ βV SortV V ini \(42\)

the back to those with an initial position at the front. This where the Sortp function outputs the initial positions in the optimization sequence makes it challenging for CAVs in order of distance from far to near in the direction of travel, intermediate positions with slower velocities to find suitable the SortV function outputs the initial velocities in increasing driving strategies, potentially leading to sub-optimal solutions, order, and the Sort function outputs the function values in or even in unsolvable situations extreme cases as illustrated increasing order. 

in Fig. 3\(a\). Furthermore, when optimization is based solely 2\) Technique for Order Preference by Similarity to Ideal on positional order, collisions in rear CAVs may render the Solution Method: In LOD method, the rankings of two factors optimization problem unsolvable. Therefore, employing this are linearly combined, which inevitably leads to the generation method imposes strict requirements on the feasibility of the of identical values. When ranking identical values, it is only initial state variables. However, the different optimization possible to follow the original order and further differentiation sequences result in different final solutions. Since each CAV

is not possible, thus affecting the final result. To avoid this cannot alter the driving strategy of other CAVs during indi-issue, a method using technique for order preference by sim-vidual optimization, it can only choose to yield or overtake ilarity to ideal solution method \(TOPSIS\) has been proposed, to avoid collision. Therefore, different optimization sequences which fully utilizes the comprehensive evaluation of original result in different decisions for CAVs, as illustrated in Fig. 

data to accurately reflect the differences between evaluation

3\(b\). The appropriate optimization sequence is crucial for the schemes. This method is mainly divided into the following efficiency and quality of the solution. 

three steps:

To address the issue of unsolvable optimization problems

• Step 1: Positive direction transformation of the original in extreme situations and to remove the strict limitations on matrix. 

the feasibility of the initial decision variables, we propose

• Step 2: Normalization of positive matrix. 

an improved algorithm based on Algorithm 1. We evaluate

• Step 3: Calculate scores. 

the optimization priority for each CAV and provide an opti-The purpose of Step 1 is to normalize the original indices, mization ranking to improve the efficiency and quality of the i.e., to convert the indices into maximization type indices, 

9

so that all indices are aligned in the same direction. In Algorithm 2 Linearized and Enhanced Optimization Order this problem, we introduce the initial data matrix M as Determination Algorithm

M = pini, V ini, where pini = pini, pini, ..., piniT

T

1

2

and

N

Input: Initial Position pini = pini, pini, ..., pini 1

2

, Initial

N

V ini = V ini, V ini, ..., V iniT

T

1

2

. As aforementioned, when de-

N

Velocity V ini = V ini, V ini, ..., V ini

, β

1

2

N

p, βV

termining the optimization sequence, we first optimize CAVs Output: Order of Optimization

that are located closer to the front and have slower velocities. 

1: Orderpini = Sortp pini

Therefore, the indicator after normalization can be represented 2: OrderV ini = SortV V ini

as:

3: for i = 1 to N do

¯

pini = pini, 

4:

Orderi,p = f ind Orderpini == i

¯

V ini = max V ini − V ini, 

\(43\)

i

i

5:

Orderi,V = f ind \(OrderV ini == i\)

¯

M = ¯

pini, ¯

V ini . 

6:

V aluei = βpOrderi,pini \+ βV Orderi,V ini 7: end for

After normalization, the requirements for priority optimiza-8: OrderLOD = Sort \(V alue\)

tion are satisfied better if the value of ¯

pini and ¯

V ini are larger. 

i

9: ¯

pini = pini

However, the units of the two values are currently different. In 10: for i = 1 to N do

order to eliminate the units influence, Step 2 normalizes the 11:

¯

V ini = max V ini − V ini

i

i

positive matrix. We define the element in the i-th row and j-th 12: end for

column of the positive direction transformation matrix ¯

M as

13:

¯

M = ¯

pini, ¯

V ini

mij, and the normalization method is represented as: 14: β1 = βp, β2 = βV

m



15: for i = 1 to N do

ij − min

¯

Mj

ˇ

mij =

\(44\)

16:

for j = 1 to 2 do

max

¯

M 



j

− min

¯

Mj





17:

ˇ

mij = mij −min

¯

Mj / max ¯

Mj −min

¯

Mj

where ¯

Mj represents the elements of the j-th column of the q

positive direction transformation matrix ¯

M. 



2

18:

D\+ =

β

− ˇ

m

i

j

max

¯

Mj

ij

In Step 3, we calculate the distance between the normalized q

2

19:

D− =

β

positive matrix and the maximum and minimum values to i

j

ˇ

mij − min

¯

Mj

D−

obtain scores. The scores are used for sorting based on their 20:

S

i

i = D\+\+D−

magnitude. We define its distance from the maximum and i

i

21:

end for

minimum values as D\+ and D−, respectively, which can be i

i

22: end for

represented as:

23: OrderT OP SIS = Sort Si in descending order q

D\+ =

β

− ˇ

m 2, 

i

j

max

¯

Mj

ij

\(45\)

q

D− =

β

2

In this case, the optimization can be performed based on the i

j

ˇ

mij − min

¯

Mj

Order obtained using the two methods mentioned above. 

where βj is the weight value corresponding to the j-th column. 

With these techniques, the sequential Gauss-Seidel algo-With D\+ and D−, the score can be calculated as: i

i

rithm for cooperative decision-making is shown in Algorithm

3. 

D−

S

i

i =

. 

\(46\)

D\+ \+ D−

i

i

C. Trajectory Planning

The final priority can be obtained by arranging the score Si in descending order. 

In the previous sections, we get the vector of decision The LOD and TOPSIS algorithms are shown in Algorithm variables. The paths and the time related to the nodes can serve

2. To remove the strict limitations on the feasibility of the as good references for generating collision-free and feasible initial decision variables, we propose an algorithm to detect the trajectories for every CAV. In this section, we regard time number of collisions each CAV generates with other CAVs in variables tv and path variables P e computed by the methods i

i

the initial state and determine an optimization order according we proposed in previous section as references, and formulate to this. Due to the randomness of the initial state, it is difficult an optimal control problem to generate a trajectory for every for each CAV to avoid collisions with other CAVs. Therefore, CAV. The kinematic and control input constraints are the main in each iteration, we sort the optimization order of CAVs considerations in this process. 

OrderCol based on the number of collisions. CAVs with a 1\) Kinematic Constraints: For all CAVs, we adopt a higher number of collisions have more complex interaction discrete-time bicycle motion model with a constant time relationships, requiring more time for optimization and are interval τs. In the constraints, we assume that the initial time easily influenced by decisions of other CAVs. Therefore, CAVs steps of all CAVs are aligned with each other, with an initial with fewer collisions are prioritized for optimization to avoid time tsi = 0. However, the duration of the generated CAV

i

repeated optimization of CAVs with higher collision counts. 

reference points is different, so to ensure that the generated When the number of collisions is 0 for all CAVs during the trajectories have the same duration, we can use the shortest iteration, it indicates that the current state is a feasible solution. 

trajectory as a standard to trim the other trajectories. Therefore, 

10

Algorithm 3 Sequential Gauss-Seidel Algorithm for Cooper-3\) Reference Path: We use linear interpolation to generate ative Decision-Making

the reference point positions at each time step. Specifically, 1: Randomly choose an initial state x\(0\), set k = 0, sign = 0

the corresponding reference point positions are: 2: Obtain the Order using Algorithm 2

τ × τs − tk

tk\+1 − τ × τs

3: while sign ̸= 1 do

ˆ

pτ,ref =

i pk\+1 \+ i

pk, 

i

i

i

4:

Sort the order Order

tk\+1 − tk

tk\+1 − tk

Col according to the number of

i

i

i

i

\(50\)

collisions using \(29\) and \(30\)

∀k ∈ \{0, 1, ..., mi\} , tk ≤ τ × τ

, 

i

s ≤ tk\+1

i

5:

for all i ∈ OrderCol do

∀i ∈ N , ∀τ ∈ Ti. 

6:

Solve the MILP problem of \(37\) with x \(k\) and get a solution of ˇ

xi \(x−i \(k\)\)

ˆ

pτ,ref is the position of the center point of CAV i, but in the i

7:

△Ji \(k\) = Ji \(xi \(k\)\) − Ji \(ˇ

xi \(k\)\)

constraints of the motion model, the position of the point refers \( ˇx

to the position of the rear axle center of the CAV. Therefore, i \(k\) , 

if △Ji ≥ ε

8:

xi \(k \+ 1\) =

x

the position of the reference point needs to be moved and i \(k\) , 

else

transformed to the rear axle center. Thus, the derived position 9:

x \(k \+ 1\) = \(xi \(k \+ 1\) , x−i \(k\)\)

after the transformation is:

10:

end for

11:

if x \(k \+ 1\) = x \(k\) then

pk\+1 − pk

pτ,ref = ˆ

pτ,ref − d

i

i

, 

12:

sign = 1

i

i

i 



pk\+1 − pk

i

i 2

13:

end if

\(51\)

∀k ∈ \{0, 1, ..., m

≤ τ × τ

, 

14:

k = k \+ 1

i\} , tk

i

s ≤ tk\+1

i

15: end while

∀i ∈ N , ∀τ ∈ Ti

where di is the distance between the center point and the rear axle center point and ∥ ∥ represents the 2-norm. 

the initial time steps of all CAVs in the next planning period 2

4\) Optimal Control Formulation: With above definition, we are still consistent. 

formulate the optimal control problem for each CAV as : We denote the reference path of CAV i obtained from solving methods as vk , where vk is the k-th vertex that τi

τi−1

i

i

X 

T





X

CAV i passes through in the path, and k ∈ 0, 1, ..., mi . For min

xτ − xτ,ref

Q xτ − xτ,ref

\+

\(uτ \)T Ruτ , 

i

i

i

i

i

i

uτ

i

simplicity, we denote the time required for CAV i to reach vk τ =0

τ =0

i

from the center as tk, and the corresponding position of vk s.t. 

\(47\), \(49\). 

i

i

as pk. Furthermore, we assume t0 = 0 for all i ∈ N , with \(52\)

i

i

the first time step being 0. Then the last time step of CAV i The objective function takes the deviations of actual trajecto-is τ

ries from the reference and control input into consideration. 

i = ⌊tmi /τ

i

s⌋, where ⌊·⌋ represents the floor function. The h

iT

set of all time steps for CAV i is denoted as Ti = \[0, 1, ..., τi\]. 

In particular, xτ,ref =

pτ,x,ref , pτ,y,ref , θτ,ref , V τ,ref

, 

i

i

i

i

i

The state vector xτ , τ

∈

T

=

i

i

is defined as xτi

where pτ,x,ref and pτ,y,ref represent the X and Y coordinates i

i

pτ , pτ , θτ , V τ T . pτ

and pτ

represent the X and Y

i,x

i,y

i

i

i,x

i,y

of reference paths in the global coordinate system, respec-coordinates of the CAV’s rear axle center in the global tively, θτ,ref is the reference heading angle and V τ,ref is the i

i

coordinate system, while θτ represents the heading angle, and i

reference velocity. Q is positive semi-definite and R is positive V τ represents the longitudinal velocity. The control inputs are i

definite. For each CAV i, solving \(52\) can obtain a feasible denoted as uτ = \[δτ , aτ \]T , where δτ is the steering angle, and i

i

i

i

and collision-free trajectory. 

aτ is the acceleration. With above definition, the discrete-time i

bicycle motion model \[39\] can be expressed as: V. EXPERIMENT RESULTS

pτ\+1 = pτ \+ fr \(δτ , V τ \) cos \(θτ \) , For verifying the effectiveness of the proposed method, 



i,x

i,x

i

i

i





pτ \+1 = pτ

\+ f

, V τ \) sin \(θτ \) , 

three common urban traffic scenarios are designed in this i,y

i,y

r \(δτ

i

i

i

\(47\)

θτ\+1 = θτ \+ arcsin \(τ

sin \(δτ \) /b

section. Gurobi \[40\] and CasADi \[41\] are used to solve \(36\)



i

i

sV τ

i

i

i\) , 





and \(52\), respectively. The relevant parameter settings are

V τ\+1 = V τ \+ τ

i

i

saτ

i

shown in Table I. The matrices Q and R in the problem are where bi is the wheelbase of the CAV i and fr \(δτ , vτ \) is the set as: Q = diag\(20, 20, 0, 0\) and R = diag\(20, 0.1\). 

i

i

function defined as:

For each scenario, we have set up three types of exper-q

iments. The first type of experiment visually demonstrates fr \(δ, V \) = b \+ τsV cos δ −

b2 − \(τsV sin \(δ\)\)2. 

\(48\)

the algorithm’s effectiveness in reducing the total cost and 2\) Control Input Constraints: Due to physical limitations the impact of each constraint in a single trial. The conver-on engine force, braking force, and wheel angles, the following gence is reflected by the average cost change per iteration. 

constraints need to be applied to the control inputs: The second type of experiment is a quantitative study. We conduct 25 sets of experiments using different methods we δmin ≤ δτ ≤ δmax, 

i

i

i

proposed with random initial states, where we add a Gauss amin ≤ aτ ≤ amax, 

\(49\)

i

i

i

distribution to the initial velocities V ini. This can be expressed

∀i ∈ N , ∀τ ∈ T

as ˜

V ini = V ini \+ λ, where λ ∼ N \(0, 32\). We evaluate the i. 





11

\(a\) Way-Point Graph

\(b\) Initial Position

\(c\) t = 0.5 s

\(d\) t = 3.6 s

\(e\) t = 5.4 s

\(f\) t = 0.8 s

\(g\) t = 3.6 s

\(h\) t = 4.6 s

\(i\) t = 5.4 s

Fig. 4. Simulation results for the overtaking scenario. 

TABLE I

PARAMETER SETTINGS USED IN SIMULATIONS

Param. 

Value

Param. 

Value

Param. 

Value

γmax

3.0 m/s2

γmin

−4.5 m/s2

ηmax

3.0 m/s2

αt

0.1

αV

1.0

αa

0.5

αθ

0.5

τs

0.1 s

b

2.405 m

dsafe

2.366 m

L

3.526 m

W

1.673 m

amax

4.0 m/s2

amin

−6.0 m/s2

ϵ

0.2

δmax

0.9 rad

δmin

−0.9 rad

βp, βV

0.5

algorithm efficiency of the proposed algorithm by the time to solve the ε-MINE and the average time TAver per iteration. 

In the third type of experiment, we conduct an additional 10

sets of experiments using the methods we proposed and MILP

method, with the same experimental setup as the second group of experiments. All the experiments are conducted with an Intel Core i7-9750H processor in MATLAB. 

Fig. 5. 

Velocity, acceleration, and steering angle of all CAVs for the overtaking scenario. 

A. Overtaking

In this section, we demonstrate examples of CAVs overTABLE II

taking on a one-way two-lane road. We sample along the COMPARISON OF COMPUTING TIME AND COST VALUE AMONG DIFFERENT

centerline of the lane with a spacing of 10 m. Each sampled METHODS IN DIFFERENT OPTIMIZATION ORDERS FOR THE OVERTAKING

SCENARIO. 

waypoint is connected to the two nearest waypoints on the adjacent lane in the direction of travel to form edges. Each Methods

TOPSIS Order

Linear Order

Default Order

lane is 3.75 m wide. The plotted way-point graph is shown Computing Time

2.37 s

2.41 s

2.87 s

T

in the Fig. 4\(a\) and the initial positions of each CAV are Aver

0.57 s

0.58 s

0.59 s

JAver

2.0

2.0

2.7

shown in the Fig. 4\(b\). The initial speed V ini of CAV1-4

Success Rate

22/25

22/25

22/25

are 18 m/s, 12 m/s, 12 m/s, and 8 m/s, respectively, and the reference velocity V r are set as the same as the initial speed i

with distribution ˜

V ini. The velocity range for all CAVs are at t = 0.5 s, have been modified to more reasonable actions, h

i

defined as 0.6 ˜

V ini, 1.3 ˜

V ini , which represents the minimum such as maintaining a straight trajectory. Potential collisions velocity V min and maximum velocity V max, respectively. 

are averted by CAV3 adjusting lanes after advancing a certain In the first experiment, it is evident that the speed of the distance and CAV2 changing lanes only after CAV1 has safely rear CAV is much greater than that of the front CAV, and passed. Since CAV4 has the slowest speed, both CAV2 and CAV2 and CAV3 occupy two lanes. Therefore, to achieve CAV3 use the lane-changing overtaking method to overtake collision-free safe driving, a coordinated strategy is crucial. 

CAV4 and avoid collisions. The circles of different colors To demonstrate the effectiveness of the proposed algorithm, represent the trajectories of the corresponding CAVs. The we randomly assign initial states, with the initial decision average cost decreased from the initial value of 7.89 to 3.93

strategies as shown in the Fig. 4\(c\)-\(e\). It can be observed after 4 iterations, resulting in a 50% reduction in average cost. 

that in the initial decision strategies, a collision between Fig. 5 shows the changes in speed, acceleration, and steering CAV1 and CAV3 occurs at t = 3.6 s, and throughout the wheel angle. 

driving process, CAVs exhibit unreasonable lane-changing The results of the second experiment are shown in Table behavior. Results are shown in Fig. 4\(f\)-\(i\). Unreasonable

II, where default order refers to the sequential arrangement of lane-changing behaviors, as exhibited by CAV2 and CAV3

CAVs from left to right according to their initial positions, as



12

TABLE III

COMPARISON OF COMPUTING TIME AND COST VALUE AMONG DIFFERENT

METHODS IN DIFFERENT OPTIMIZATION ORDER FOR THE ROUNDABOUT

SCENARIO. 

Methods

TOPSIS Order

Linear Order

Default Order

Computing Time

1.56 s

1.93 s

1.95 s

TAver

0.52 s

0.61 s

0.62 s

JAver

5.4

5.4

5.4

Success Rate

25/25

25/25

25/25

B. Roundabout

In this section, we demonstrate an example of cooperative decision-making for multiple CAVs on a roundabout. The waypoint graph is shown in the Fig. 6\(a\), where we sample along the center line of the roads and connect each sampled waypoint with the two nearest waypoints on different lanes in the driving direction to form edges. Fig. 6\(f\) shows the initial positions Fig. 7. 

Velocity, acceleration, and steering angle of all CAVs for the roundabout scenario. 

of each CAV. The initial velocities V ini of the CAV1-4 are assigned as 7 m/s, 7 m/s, 4 m/s, and 7 m/s, with a reference speed set as the initial speed with distribution ˜

V ini, and the

shown in the Fig. 4\(b\). TAver represents the computational maximum velocity V max and minimum velocity V min are time per iteration and JAver represents the final cost per 0.6 ˜

V ini, 1.3 ˜

V ini, respectively. 

CAV. We represent this optimization sequence using the array We randomly assign initial states to all CAVs, and the

\[1, 2, 3, 4\], where the numbers correspond to the CAV indices initial decision strategies are shown in the Fig. 6\(b\)-\(e\). It arranged in the order of optimization from left to right. 

can be observed that in the initial decision strategies, there Obviously, the optimization order has a impact on the are still unreasonable lane-changing behaviors, such as CAV4

computing time and in some conditions, it influence the changing lanes downwards at t = 3.5 s. The optimized strategy effectiveness of the algorithm. In this scenario, by prioritizing is shown in the Fig. 6\(g\)-\(j\) after algorithm processing, the optimization of the front CAVs, redundant optimization of unreasonable lane-changing behaviors are changed, and CAV2

strategies can be avoided, resulting in the highest efficiency chooses to change lanes while closely following CAV1 with in problem-solving. 

the same speed to ensure that the speed remains stable at the



13

TABLE IV

COMPARISON OF COMPUTING TIME AND COST VALUE AMONG DIFFERENT

METHODS IN DIFFERENT OPTIMIZATION ORDER FOR THE UNSIGNALIZED

INTERSECTION SCENARIO. 

Methods

TOPSIS Order

Linear Order

Default Order

Computing Time

9.21 s

9.23 s

9.22 s

TAver

3.07 s

3.08 s

3.07 s

JAver

9.7

9.7

9.7

Success Rate

25/25

25/25

25/25

initial speed. At the same time, this strategy reduces the lane-changing behavior of the slower CAV3, so that the velocities of all CAVs require minimal adjustment, as shown in the Fig. 7, to reduce braking or acceleration actions. The average cost decreased from the initial value of 15.27 to 8.34 after 4

iterations, resulting in a 45% reduction in average cost. 

The results of different optimization orders are shown in Table III, where default order refers to the sequential arrange-Fig. 9. 

Velocity, acceleration, and steering angle of all CAVs for the ment of CAVs from left to right according to their initial unsignalized intersection scenario

positions, as shown in the Fig. 6\(f\). The TOPSIS method still have the best performance. However, the shortcoming of the linear method leads to worse performance. 

the Fig. 8\(e\). The initial velocities V ini of the CAVs are all 10 m/s, with a reference speed equal to the initial speed C. Unsignalized Intersection

with distribution ˜

V ini, and the maximum velocity V max and In this section, we show an example of cooperative decision-minimum velocity V min are 0.6 ˜

V ini, 1.3 ˜

V ini, respectively. 

making for multiple CAVs at an unsignalized intersection. 

In this scenario, we assume that CAV6 and CAV7 intend to In this scenario, we only consider left turn and straight turn left and other CAVs intend to go stright. We randomly through movements. Each lane is 3.75 m wide, and we sample assign an initial state, and the initial strategies are shown in points equidistant along the centerline of the road for the the Fig. 8\(b\)-\(d\). In the initial state, the CAV6 and CAV7 are straight segments. Each sampled point is connected to the involved in a collision at t = 1.6 s and other CAVs exhibit two nearest points on different lanes in the direction of travel many ineffective and irrational lane-changing behaviors, such to form edges. To demonstrate the effectiveness of the way-as CAV1 at t = 1.6 s and t = 4.1 s, which can lead to higher point graph, we only show the straight-through and left-turn fuel consumption and may potentially cause safety accidents. 

movements at the bottom right intersection, as shown in the After the algorithm processing, the strategies are adjusted Fig. 8\(a\). The initial positions of each CAV are shown in as shown in the Fig. 8\(f\)-\(h\), where the CAVs avoid the

14

TABLE V

Gauss-Seidel algorithms for iteration, thereby deriving the COMPARISON OF COMPUTING TIME AND COST VALUE AMONG DIFFERENT

trajectories for each CAV. To validate the effectiveness of MODELS TO OBTAIN DECISION-MAKING VARIABLES FOR THE THREE

this method, simulations are conducted for three urban traffic DIFFERENT SCENARIOS

scenarios with significantly different topological structures. 

Simulation results demonstrate that the proposed optimization Decision-Making Model Type

MILP

MIPG

scheme can efficiently generate more reasonable strategies for Overtaking

8.85 s

3.03 s

Roundabout

32.40 s

2.68 s

CAVs, and the generalization ability of the proposed method Unsignalized Intersection

69.13 s

6.83 s

is appropriately verified. Furthermore, it is shown that the \(a\) Computing Time

proposed sequential Gauss-Seidel algorithms can improve the computational efficiency compared to the baseline methods. 

Decision-Making Model Type

MILP

MIPG

Overtaking

7.8

11.0

Roundabout

34.7

35.6

R

Unsignalized Intersection

41.9

44.5

EFERENCES

\(b\) Cost Value

\[1\] D. Omeiza, H. Webb, M. Jirotka, and L. Kunze, “Explanations in Autonomous Driving: A Survey,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 8, pp. 10142–10162, 2021. 

collision and retain only necessary lane-changing behaviors. 

\[2\] A. Broggi, M. Buzzoni, S. Debattisti, P. Grisleri, M. C. Laghi, P. Medici, and P. Versari, “Extensive Tests of Autonomous Driving Technologies,” 

For example, at t = 1.6 s, CAV6 in the process of turing left IEEE Trans. Intell. Transp. Syst., vol. 14, no. 3, pp. 1403–1415, 2013. 

and keep the lane while CAV7 chooses to change lanes to

\[3\] J. Ma, Z. Cheng, X. Zhang, M. Tomizuka, and T. H. Lee, “Alternating avoid collision. From the speed profiles in the Fig. 9, it can Direction Method of Multipliers for cConstrained Iterative LQR in Autonomous Driving,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 12, be observed that CAV5 slows down to avoid CAV2 and CAV4. 

pp. 23031–23042, 2022. 

The average cost decreased from the initial value of 12.73 to

\[4\] Z. Zhong, E. E. Lee, M. Nejad, and J. Lee, “Influence of CAV

8.59 after 4 iterations, resulting in a 33% reduction in average Clustering Strategies on Mixed Traffic Flow Characteristics: An Analysis of Vehicle Trajectory Data,” Transportation Research Part C: Emerging cost. 

Technologies, vol. 115, p. 102611, 2020. 

The results of the second experiment are shown in Table

\[5\] X. Sun, F. R. Yu, and P. Zhang, “A Survey on Cyber-Security of

IV. To demonstrate the effectiveness of the method, we Connected and Autonomous Vehicles \(CAVs\),” IEEE Trans. Intell. 

Transp. Syst., vol. 23, no. 7, pp. 6240–6259, 2021. 

correspondingly arrange the positions in the initial sorting, as

\[6\] M. Noor-A-Rahim, Z. Liu, H. Lee, M. O. Khyam, J. He, D. Pesch, shown in the Fig. 8\(e\). Due to the initial velocities being too K. Moessner, W. Saad, and H. V. Poor, “6G for Vehicle-to-Everything close and multiple cars being relatively close to their initial \(V2X\) Communications: Enabling Technologies, Challenges, and Op-portunities,” Proc. IEEE, vol. 110, no. 6, pp. 712–734, 2022. 

positions, the differences in the results obtained by the three

\[7\] K. Abboud, H. A. Omar, and W. Zhuang, “Interworking of DSRC and methods are not significant. 

Cellular Network Technologies for V2X Communications: A Survey,” 

IEEE Trans. Veh. Technol., vol. 65, no. 12, pp. 9457–9470, 2016. 

\[8\] Z. Huang, S. Shen, and J. Ma, “Decentralized iLQR for Cooperative D. Comparison of Different Decision-Making Models Trajectory Planning of Connected Autonomous Vehicles via Dual Consensus ADMM,” IEEE Trans. Intell. Transp. Syst., 2023. 

In this section, we set up a series of experiments to compare

\[9\] H. Liu, Z. Huang, Z. Zhu, Y. Li, S. Shen, and J. Ma, “Improved the solution efficiency and quality of the two models, MIPG

Consensus ADMM for Cooperative Motion Planning of Large-Scale Connected Autonomous Vehicles with Limited Communication,” IEEE

and MILP. The MIPG problem is solved by the sequential T. Intell. Veh., 2024. 

Gauss-Seidel algorithm we proposed before and the MILP

\[10\] X. Zhang, Z. Cheng, J. Ma, S. Huang, F. L. Lewis, and T. H. 

problem is solved by the Gurobi. The results are shown in Lee, “Semi-Definite Relaxation-Based ADMM for Cooperative Planning Table V. It is evident from the experimental results that the and Control of Connected Autonomous Vehicles,” IEEE Trans. Intell. 

Transp. Syst., vol. 23, no. 7, pp. 9240–9251, 2021. 

Nash equilibrium solution of the MIPG problem and the

\[11\] Z. Li, Q. Wang, J. Wang, and Z. He, “A Flexible Cooperative MARL

globally optimal solution of the MILP problem show slight Method for Efficient Passage of an Emergency CAV in Mixed Traffic,” 

differences in solution quality. The cost value of the two IEEE Trans. Intell. Transp. Syst., 2024. 

\[12\] P. Lv, J. Han, J. Nie, Y. Zhang, J. Xu, C. Cai, and Z. Chen, “Coop-solutions have a slight difference, and as the complexity of erative Decision-Making of Connected and Autonomous Vehicles in an the scenario increases, the cost difference decreases. Based Emergency,” IEEE Transactions on Vehicular Technology, vol. 72, no. 2, on the previous definitions, we can easily find that adjusting pp. 1464–1477, 2022. 

\[13\] J. Zhang, S. Li, and L. Li, “Coordinating CAV Swarms at Intersections the parameter ϵ can help reduce this gap. However, solving the With a Deep Learning Model,” IEEE Trans. Intell. Transp. Syst., vol. 24, MILP problem takes much longer time than solving the MIPG

no. 6, pp. 6280–6291, 2023. 

problem with the method we proposed, especially as road

\[14\] S. Li, K. Shu, Y. Zhou, D. Cao, and B. Ran, “Cooperative Critical Turning Point-Based Decision-Making and Planning for CAVH Intersection structures become more complex and the number of CAVs Management System,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 8, increases. 

pp. 11062–11072, 2022. 

\[15\] Y. Meng, L. Li, F.-Y. Wang, K. Li, and Z. Li, “Analysis of Cooperative Driving Strategies for Nonsignalized Intersections,” IEEE Trans. Veh. 

VI. CONCLUSION

Technol., vol. 67, no. 4, pp. 2900–2911, 2017. 

\[16\] X. Duan, C. Sun, D. Tian, J. Zhou, and D. Cao, “Cooperative Lane-This paper proposes a decision-making approach to ad-Change Motion Planning for Connected and Automated Vehicle Platoons dress the cooperative decision-making problem of CAVs in in Multi-Lane Scenarios,” IEEE Trans. Intell. Transp. Syst., vol. 24, diverse urban traffic scenarios with a generic road topol-no. 7, pp. 7073–7091, 2023. 

\[17\] S. A. Fayazi and A. Vahidi, “Mixed-Integer Linear Programming for ogy. The problem is modeled as an MIPG, and the Nash Optimal Scheduling of Autonomous Vehicle Intersection Crossing,” 

equilibrium solution is obtained by employing the proposed IEEE T. Intell. Veh., vol. 3, no. 3, pp. 287–299, 2018. 

15

\[18\] M. Tajalli and A. Hajbabaie, “Traffic Signal Timing and Trajectory

\[41\] J. A. E. Andersson, J. Gillis, G. Horn, J. B. Rawlings, and M. Diehl, Optimization in a Mixed Autonomy Traffic Stream,” IEEE Trans. Intell. 

“CasADi – A Software Framework for Nonlinear Optimization and Transp. Syst., vol. 23, no. 7, pp. 6525–6538, 2021. 

Optimal Control,” Math. Program. Comput., 2018. 

\[19\] R. A. Dollar and A. Vahidi, “Multilane Automated Driving with Optimal Control and Mixed-Integer Programming,” IEEE Trans. Control Syst. 

Technol., vol. 29, no. 6, pp. 2561–2574, 2021. 

\[20\] K.-F. Chu, A. Y. S. Lam, and V. O. K. Li, “Dynamic Lane Reversal Routing and Scheduling for Connected and Autonomous Vehicles: Formulation and Distributed Algorithm,” IEEE Trans. Intell. Transp. 

Syst., vol. 21, no. 6, pp. 2557–2570, 2020. 

\[21\] Z. Yao, H. Jiang, Y. Cheng, Y. Jiang, and B. Ran, “Integrated Schedule and Trajectory Optimization for Connected Automated Vehicles in a Conflict Zone,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 3, pp. 1841–1851, 2022. 

\[22\] Z. Qin, A. Ji, Z. Sun, G. Wu, P. Hao, and X. Liao, “Game Theoretic Application to Intersection Management: A Literature Review,” IEEE

Transactions on Intelligent Vehicles, 2024. 

\[23\] P. Hang, C. Lv, C. Huang, Y. Xing, and Z. Hu, “Cooperative Decision Making of Connected Automated Vehicles at Multi-Lane Merging Zone: A Coalitional Game Approach,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 4, pp. 3829–3841, 2021. 

\[24\] P. Hang, C. Huang, Z. Hu, and C. Lv, “Decision Making for Connected Automated Vehicles at Urban Intersections Considering Social and Individual Benefits,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 11, pp. 22549–22562, 2022. 

\[25\] P. Hang, C. Huang, Z. Hu, Y. Xing, and C. Lv, “Decision Making of Connected Automated Vehicles at an Unsignalized Roundabout Considering Personalized Driving Behaviours,” IEEE Trans. Veh. Technol., vol. 70, no. 5, pp. 4051–4064, 2021. 

\[26\] Y. Luo, Y. Xiang, K. Cao, and K. Li, “A Dynamic Automated Lane Change Maneuver Based on Vehicle-to-Vehicle Communication,” 

Transp. Res. Pt. C-Emerg. Technol., vol. 62, pp. 87–102, 2016. 

\[27\] E. Amini, A. Omidvar, and L. Elefteriadou, “Optimizing Operations at Freeway Weaves with Connected and Automated Vehicles,” Transp. Res. 

Pt. C-Emerg. Technol., vol. 126, p. 103072, 2021. 

\[28\] J. Huang, Z. Wu, W. Xue, D. Lin, and Y. Chen, “Non-Cooperative and Cooperative Driving Strategies at Unsignalized Intersections: A Robust Differential Game Approach,” IEEE Trans. Intell. Transp. Syst., 2024. 

\[29\] X. Pan, B. Chen, S. Timotheou, and S. A. Evangelou, “A Convex Optimal Control Framework for Autonomous Vehicle Intersection Crossing,” 

IEEE Trans. Intell. Transp. Syst., vol. 24, no. 1, pp. 163–177, 2022. 

\[30\] Y. Rahmati, M. K. Hosseini, and A. Talebpour, “Helping Automated Vehicles With Left-Turn Maneuvers: A Game Theory-Based Decision Framework for Conflicting Maneuvers at Intersections,” IEEE Trans. 

Intell. Transp. Syst., vol. 23, no. 8, pp. 11877–11890, 2021. 

\[31\] J. F. Medina-Lee, J. Godoy, A. Artu˜nedo, and J. Villagra, “Speed Profile Generation Strategy for Efficient Merging of Automated Vehicles on Roundabouts With Realistic Traffic,” IEEE T. Intell. Veh., vol. 8, no. 3, pp. 2448–2462, 2022. 

\[32\] S. Alighanbari and N. L. Azad, “Multi-vehicle coordination and real-time control of connected and automated vehicles at roundabouts,” in IEEE Connect. Autom. Veh. Symp.\(CAVS\), pp. 1–6, 2020. 

\[33\] L. Wei, Z. Li, J. Gong, C. Gong, and J. Li, “Autonomous Driving Strategies at Intersections: Scenarios, State-of-the-Art, and Future Outlooks,” 

in IEEE Conf. Intell. Transport. Syst. Proc.\(ITSC\), pp. 44–51, IEEE, 2021. 

\[34\] Z. Huang, S. Shen, and J. Ma, “A Universal Cooperative Decision-Making Framework for Connected Autonomous Vehicles with Generic Road Topologies,” arXiv preprint arXiv:2401.04968, 2024. 

\[35\] M. S. Bazaraa, J. J. Jarvis, and H. D. Sherali, Linear Programming and Network Flows. John Wiley & Sons, 2011. 

\[36\] R. E. Bixby, M. Fenelon, Z. Gu, E. Rothberg, and R. Wunderling, 

“Mixed-integer Programming: A Progress Report,” in The sharpest cut: the impact of Manfred Padberg and his work, pp. 309–325, SIAM, 2004. 

\[37\] F. Facchinei, V. Piccialli, and M. Sciandrone, “Decomposition Algorithms for Generalized Potential Games,” Comput. Optim. Appl., vol. 50, pp. 237–262, 2011. 

\[38\] S. Sagratella, “Algorithms for Generalized Potential Games with Mixed-Integer Variables,” Computational Optimization and Applications, vol. 68, no. 3, pp. 689–717, 2017. 

\[39\] P. Polack, F. Altché, B. d’Andréa Novel, and A. de La Fortelle, “The Kinematic Bicycle Model: A Consistent Model for Planning Feasible Trajectories for Autonomous Vehicles?,” in IEEE Intelligent Vehicles Symposium, pp. 812–818, 2017. 

\[40\] Gurobi Optimization, LLC, “Gurobi Optimizer Reference Manual,” 

2024. 


# Document Outline

+ Introduction 
+ Problem Formulation as Mixed-Integer Linear Programming  
	+ Way-Point Graph 
	+ Constraints  
		+ Travel Constraints 
		+ Time Constraints 
		+ Collision Avoidance Constraints 

	+ MILP Formulation 

+ Mixed-Integer Potential Game Formulation 
+ Gauss-Seidel Algorithm for Decision-Making  
	+ Gauss-Seidel Algorithm for MIPG 
	+ Sequential Gauss-Seidel Algorithm for MIPG  
		+ Linearized Optimization Order Determination Method 
		+ Technique for Order Preference by Similarity to Ideal Solution Method 

	+ Trajectory Planning  
		+ Kinematic Constraints 
		+ Control Input Constraints 
		+ Reference Path 
		+ Optimal Control Formulation 


+ Experiment Results  
	+ Overtaking 
	+ Roundabout 
	+ Unsignalized Intersection 
	+ Comparison of Different Decision-Making Models 

+ Conclusion 
+ References



