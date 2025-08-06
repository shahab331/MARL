Uncontrol ed intersection 

coordination of the 

autonomous vehicle based on 

multi-agent reinforcement 

learning. 

Isaac Arnold McSey 

Applied Data Science 

Two Year’s Master Program 

30 Credits 

2023 

Supervisor: Jan Persson 

Examiner: Johan Holmgren 

* *



* *

* *

* *

* *

* *

* *

* *



**Popular science summary **

Autonomous Vehicles \(AVs\) mark a revolutionary shift in transportation, anticipated to redefine road safety, fuel efficiency, and business dynamics. 

Intersections, however, remain challenging; they account for a significant number of accidents. Present learning methods often overlook the complexities of interactions with human-driven vehicles \(HDVs\) and pedestrians. With rising AV 

numbers, maintaining robust algorithmic interactions becomes critical. Exploration of multi-agent reinforcement learning \(MARL\), a technique that closely mirrors real-world scenarios. MARL holds promise in refining AV decisions at uncontrolled intersections. Multi-Agent Deep Deterministic Policy Gradient \(MADDPG\) proved instrumental in improving safety and comfort decisions. Incorporating global insights during training led to a 40% improvement in safety and a 20% boost in comfort at intersections. Our study aligns with the findings of various researchers emphasizing the benefits of global experiences. Using MARL promises better navigation in complex environments, potentially decreasing accidents. Global experiences expedite the learning process of AVs, ensuring adaptability to varied conditions and cultural nuances. By ensuring both efficiency and passenger comfort, this method can instill greater trust in AVs amongst the public. Embedding MADDPG 

models with global experiences emerges as a transformative approach for autonomous driving, promoting a safer and more efficient transportation landscape. 

* *

* *

* * 





i 





ii 

**Abstract **

*This study explores the application of multi-agent reinforcement learning \(MARL\) to* *enhance the decision-making, safety, and passenger comfort of Autonomous Vehicles \(AVs\)* *at uncontrolled intersections. The research aims to assess the potential of MARL in modeling* *multiple agents interacting within a shared environment, reflecting real-world situations* *where AVs interact with multiple actors. The findings suggest that AVs trained using a* *MARL approach with global experiences can better navigate intersection scenarios than* *AVs trained on local \(individual\) experiences. This capability is a critical precursor to* *achieving Level 5 autonomy, where vehicles are expected to manage all aspects of the* *driving task under al conditions. The research contributes to the ongoing discourse on* *enhancing autonomous vehicle technology through multi-agent reinforcement learning* *and informs the development of sophisticated training methodologies for autonomous* *driving. *

* *

* *

* *

* *





iii 





iv 

**Contents **

Popular science summary ........................................................................................... i 

Abstract ....................................................................................................................... iii 

LIST OF FIGURES ........................................................................................................ vii 

LIST OF TABLES ......................................................................................................... vii 

1. Introduction ............................................................................................................. 1 

1.1. Background ....................................................................................................... 1 

1.2. Research Goals and Motivation ....................................................................... 1 

1.3. Research Questions .......................................................................................... 2 

1.4. Purpose, and Objectives ................................................................................... 2 

2. Theoretical Background ......................................................................................... 4 

2.1. Deep Reinforcement Learning Algorithms .................................................... 4 

2.2. Multi-agent Frameworks ................................................................................. 5 

2.3. Cooperative MARL ........................................................................................... 5 

2.4. Algorithms in Cooperative MARL ................................................................... 6 

3. Literature Review .................................................................................................... 7 

3.1. History of Autonomous Vehicle ...................................................................... 7 

3.2. Emerging Technologies in AV industry. ......................................................... 7 

3.3. Intersection and Autonomous Vehicles .......................................................... 8 

3.4. Safety and Comfort Decision-Making in Autonomous Vehicles ................... 9 

3.5. Reinforcement Learning ................................................................................ 10 

3.6. Multi Agent Reinforcement Learning \(MARL\) ............................................. 11 

3.7. Overview of Simulators ................................................................................. 13 

4. Research Methodology ......................................................................................... 15 

4.1. Design Science ................................................................................................ 15 

4.2. Application of design science in this research ............................................. 16 

5. Design and Implementation ................................................................................. 17 

5.1. Deep Deterministic Policy Gradient Algorithm ........................................... 17 

5.2. Multi-agent Deep Deterministic Policy Gradient ......................................... 18 

5.2. Cooperative MADDPG Policy for Global Shared Experience Buffer ........... 19 

5.3. Learning Policy ............................................................................................... 19 

5.4. Rewards Definition ........................................................................................ 19 

5.5. The Simulated Environment ......................................................................... 20 

6. Design Validation and Demonstration ................................................................... 23 

v 

6.1. Training Simulation Environment Setup and Description ............................. 23 

7. Model Evaluation in Simulated Environment ..................................................... 24 

8. Results .................................................................................................................... 26 

9. Analysis and Discussion ........................................................................................ 31 

9.1. Evaluating the Models’ Safety and Comfort Decision-making Ability in 

a Four-way Uncontrolled Intersection with an HDV \(adversarial driver\) ....... 31 

9.2. Comparing Training Rewards for Shared and Individual Learning ........... 32 

Experience Algorithm ........................................................................................... 32 

9.3. Evaluation of Shared Policy Trained Agent using Two Scenarios .......... 33 

9.4. In-depth Analysis of Average PCI Metrics in Local Experiences ................ 34 

9.4. Discussion ....................................................................................................... 34 

10. Limitations, Further Studies, and Conclusion ................................................... 37 

10.1. Limitations .................................................................................................... 37 

10.2. Conclusion .................................................................................................... 37 

10.3. Future studies ............................................................................................... 38 

BIBLIOGRAPHY ......................................................................................................... 39 

APPENDIX .................................................................................................................. 45 

Implementation Details .......................................................................................... 45 

DDPG Agent Class Structure ................................................................................... 45 

Code structure and Implementation of the MADDPG Environment ..................... 46 





vi 

**LIST OF FIGURES **

Figure 1. Components of the Autonomous Vehicle .................................................. 1 

Figure 2. Different types of intersections .................................................................. 8 

Figure 3. Multi agent reinforcement learning ......................................................... 11 

Figure 4. Design Science research process \(DSRP\) model ..................................... 15 

Figure 5. MADDPG Architecture .............................................................................. 18 

Figure 6. MADDPG based on local experiences. ...................................................... 20 

Figure 7. MADDPG based on global shared experiences. ....................................... 21 

Figure 8. Components of agents in MADDPG .......................................................... 21 

Figure 9. Design validation: training scenario at a T-Junction .............................. 23 

Figure 10. Evaluation Scenario ................................................................................ 24 

Figure 11. Average reward accumulation comparison of Global and Local 

Experience Relay Buffer MADDPG Models.............................................................. 27 

Figure 12. Average reward accumulation comparison of Global and Local 

Experience Relay Buffer MADDPG Models ............................................................. 27 

Figure 13. Successful/unsuccessful \(due to collision\) rates with presence of 

an HDV \(adversarial driver\) ..................................................................................... 28 

Figure 14. Successful/unsuccessful \(due to collision\) rates with absence of an 

HDV \(adversarial driver\) .......................................................................................... 28 

Figure 15. PCI Frequency Distribution: Frequency Distribution During 

Training with Presence of Adversarial Driver ........................................................ 29 

Figure 16. PCI Frequency Distribution: Frequency Distribution During 

Evaluation without an Adversarial Driver .............................................................. 29 

Figure 17. PCI Comparison for Local experienced pool trained agents versus 

global experienced pool trained agents in the presence of an Adversarial 

driver. ......................................................................................................................... 29 

Figure 18. PCI Comparison for Local experienced pool trained agents versus 

global experienced pool trained agents in the absence of an Adversarial 

driver. ......................................................................................................................... 30 

****

**LIST OF TABLES **

Table 1: Comparing training rewards for shared and individual learning 

experience. ................................................................................................................. 26 

Table 2: Comparing training rewards for shared and individual learning 

experiences. ............................................................................................................... 32 

Table 3: Evaluation of policy-trained agent using two scenarios. ........................ 33 

Table 4: Evaluation of local experiences learning policy trained agents with 

and without adversarial driver. ............................................................................... 34 





vii 





viii 



**1. Introduction **

**1.1. Background **



*Figure 1. Components of the Autonomous Vehicle *

Autonomous Vehicles \(AVs\) embody complex systems \(see Figure 1\) demanding many components to function and make independent decisions. Their emergence, spurred by the evolution of communication and robotics, transforms our interaction with transport systems \[1\] \[2\]. AVs are projected to reduce road accidents, enhance fuel efficiency, alleviate traffic congestion, and open new business opportunities \[3\] 

\[4\]\[5\] \[6\]. It is anticipated that by 2040, AVs will account for 50% of vehicles on our road. 

However, their integration into our current transport infrastructure poses challenges, particularly at intersections where various road users interact \[7\] \[8\] \[9\]. Intersections are often hotspots for road accidents \[8\], with European and American data showing a high proportion of traffic injuries and fatalities occurring at these locations \[10\] \[11\]. The advent of AVs and intelligent transportation systems presents a potential solution. Still, the vehicles need to interpret and predict actions of human-driven vehicles \(HDVs\) and make safe decisions \[7\]\[12\]. Existing learning strategies for AVs predominantly focus on AV-only scenarios, which neglect interactions with HDVs and pedestrians \[7\]. Also, as the number of AVs increases, it’s crucial to ensure the robustness of algorithms to handle delays in data exchange and communication 

\[13\] \[14\]. 

Traditional machine learning algorithms are not optimal for these challenges, prompting exploration into deep learning, reinforcement learning, and statistical learning techniques \[15\] \[16\] \[17\] \[18\]. For instance, reinforcement learning has been used to train AVs to navigate simpler scenarios safely \[18\] \[19\], but its application to uncontrolled intersections remains unexplored. 

This study aims to explore the application of multi-agent reinforcement learning \(MARL\), which models multiple agents interacting within a shared environment \[20\]. This approach reflects the real-world situations where AVs interact with multiple actors, unlike single-agent environments \[20\] \[21\]. The research aims to assess MARL’s potential in enhancing AVs’ decision-making on safety, and passenger comfort at uncontrolled intersections, paving the way for AVs to become an integral and safe part of our transportation ecosystem. 



**1.2. Research Goals and Motivation **

The goal of our research is to integrate a Multi-Agent Reinforcement Learning \(MARL\) model into the planning layer \(See Figure 1\) of Autonomous Vehicle \(AV\) systems to enhance their decision-making and vehicle control capabilities, particularly in navigating uncontrolled intersections \[14\]. Drawing on observational data gathered from the perception layer \(as depicted in Figure 1\), the agent determines the optimal course of action, such as continuing the current trajectory or coming to a halt. After making this decision, the agent generates specific throttle and brake values to guide the vehicle’s control system. As complex systems requiring multiple functioning components, AVs hold the potential to transform our transportation landscape \[1\] \[2\] \[3\] \[4\]\[5\] \[6\] \[8\]. To further AV development, we focus on training the AI 1 

agent within a high-definition simulation environment, enabling AVs to learn to navigate safely at uncontrolled intersections by following the "Priority to the right rule". \[14\]. 

The necessity for our research arises from two challenges: the need for AVs to understand, replicate, and predict human driver behaviors and the limitation of single agent reinforcement learning \(RL\) in complex environments such as intersections. Single agent RL, while effective in stationary environments such as Atari games, has shown limitations in dynamic, high-definition simulation environments where the state transitions and rewards of one agent directly impact others, and the state and action space tends to grow exponentially \[22\]\[20\]. 

To bridge this research gap, we propose a slight variation of the Cooperative Multi-Agent Deterministic Policy Gradient \(CMADDPG\) method, building on the concept of "Centralized Planning with Decentralized Execution \(CPwDE\)." This approach involves every agent accessing its local \(individual experiences\) observations during the planning phase while a global entity supervises the system for policy updates \[22\]. During execution, the central module is removed, leaving only the agents, their policies, and local observation. This method helps to mitigate the issues associated with single-agent RL, ensuring the continual adaptation of AVs to the ever-changing environment \[22\]. However, our proposed variation is that all agents access a global\(shared\) observation\(experience\) pool during the planning. We assume that each agent gets to learn from the wider observation pool. While evaluating these two variant implementations, we will introduce an adversarial agent to ascertain the reflexive decision-making capabilities of both models. 

By implementing and evaluating these two variations and focusing on AVs traversing an unregulated intersection in our study, we aim to contribute significantly to the development of AV technologies by enabling AVs to learn cooperative behaviors in complex traffic scenarios. Furthermore, this research aspires to fill the gap in the current literature, which lacks studies on using MARL for uncontrol ed intersection navigation. As AVs will operate in complex environments alongside Human Driven Vehicles \(HDVs\), their ability to interact and collaborate wil be crucial to ensuring safe and comfortable driving experiences \[22\]\[20\]. 

We aim to provide a generalized solution for training AVs to navigate uncontrolled intersections safely and comfortably. By integrating a MARL model, we hope to enhance AVs’ capabilities, pushing them one step toward achieving full autonomy in complex traffic scenarios. 



**1.3. Research Questions **

To help achieve the aims discussed above, we ask the following research questions. 

1. How can multi-agent reinforcement learning \(MARL\) improve autonomous vehicles’ \(AVs\) safety and comfort decision-making capabilities in uncontrolled intersections, particularly in scenarios where AVs interact with HDVs \(Adversarial Drivers\)? 

2. To what extend can a MARL approach with global experiences enhance passenger safety and comfort in AVs at uncontrolled intersections compared to local \(individual\) experiences MARL? 

**1.4. Purpose, and Objectives **

As stated above, the overarching purpose of this study is to train AVs based on a Deep Reinforcement Learning \(DRL\) model in a multi-agent environment. We want to explore how AVs can handle in-the-moment \(intuition\) decision-making, for instance, meeting an adversarial driver \(driver who does not obey traffic rules\) close to HDV decision-making abilities at an uncontrolled intersection. In this regard, we aim to understand how AVs trained to cooperate at an uncontrolled intersection using MARL will work together to obey the "Priority to the right-hand rule." To reach this aim, we set out the following objectives: 1. Conduct a state-of-the-art review on AVs, RL algorithms, MARL techniques, and simulators to determine the most suitable MARL algorithm for enhancing AVs’ safe and comfortable decision-making and collaboration at uncontrolled intersections. 

2. Assess the safety and passenger comfort decision-making capabilities of autonomous vehicles \(AVs\) in uncontrolled intersections and understand the prevalent challenges when interacting with HDVs. 

3. Design and develop a multi-agent reinforcement learning \(MARL\) model tailored for improving AVs’ 

safety and comfort decision-making capabilities in uncontrol ed intersections. 

2 

4. Evaluate the MARL model’s effectiveness in simulation scenarios where AVs interact with HDVs, particularly those exhibiting adversarial or unpredictable driving behaviors. 

5. Investigate the differential impacts of training AVs using local \(individual\) experiences versus global experiences in a MARL environment. 

6. Compare AVs’ safety and comfort performance with the MARL approach incorporating global experiences against those trained with MARL models focusing only on local experiences. 

We divide our research into several distinct sections to thoroughly investigate this proposition. Section 2 

delineates the theoretical frameworks underpinning the research. 

Section 3 presents a comprehensive literature review, examining various related concepts and technologies. Section 4 explicates our research methodology in detail, including the theorizing process, the algorithms implemented, and the overarching thesis framework. Section 5 describes the design of MARL 

and its implementation, including the evaluation of the artifact. Section 6 presents the artifact validation and demonstration. Section 7 presents evaluation of the solution implemented and elaborates on the data collection process for further analysis. Section 8 presents results collected during the evaluation. Section 9 

delineates our data analysis procedures and discussion. Lastly, Section 10 concludes the paper by reflecting on the data analysis results, answering our research questions and objectives, and providing suggestions for potential future studies. Section 1 provides an overview of the study, introducing the research background, opportunity, questions and objectives, and the problem definition. 





3 

**2. Theoretical Background **

Our study concentrates on AVs traversing an uncontrolled intersection by following the "Priority to the right-hand rule." Given that the navigation of the intersection necessitates multi-AV cooperation, we interpret this circumstance as a Cooperative Multi-Agent Reinforcement Learning \(MARL\) issue. Each vehicle acts as an agent operating within a state, contributing to a collective reward. Our approach is modeled on Lowe et al.’s implementation, as outlined in their work \[22\]. 

The application of single-agent Reinforcement Learning \(RL\) is somewhat restrained due to its limitations within a stationary environment. As demonstrated in single Atari games, such stationary environments allow an agent to perform sequential actions within a static setting, yielding a fresh state and agent-related rewards. Commonly, these environments are portrayed as Markov Decision Processes \(MDPs\), which aim to maximize agent rewards \[20\]. However, this poses two distinct challenges: 1. The presumption of a stationary environment does not apply to MARL within high-definition simulators. Here, the state transitions and rewards of one agent directly impact others. 

2. The state and action space tend to grow exponentially, as explained by Lowe etal.\[22\]. 

As a result, it is not feasible to utilize single-agent RL approaches, such as Q-Learning or policy gradient. 

These methods struggle in multi-agent scenarios due to constant environmental changes and the resulting difficulties with the replay buffer. Additionally, learning accuracy becomes problematic as previously optimized learned experiences lose their efficacy in new environments. Moreover, policy gradient algorithms in a MARL that necessitate coordination, as exemplified in intersection scenarios, involve high variance gradient estimates \[22\]. 

Several potential solutions to these issues lie within the framework of "Centralized Planning with Decentralized Execution." In centralized planning, every agent can access its local observations. In our study context, this means an image of the environment and the relative positioning of other agents \(vehicles\) within the intersection. Despite agents only possessing local data and policies for training, a global entity supervises the entire system, guiding policy updates. This mechanism mitigates the impact of non-stationarity, as agents learn with the assistance of a globally informed module. 

Conversely, in decentralized execution, the central module is removed during testing, leaving only the agents, their policies, and local observation. This arrangement helps mitigate the issues related to an expanding state and action space, as joint policies are not explicitly learned. We posit that the central module would furnish enough information to direct local policy training, ensuring it is optimal for the whole system once testing commences \[22\]. 



**2.1. Deep Reinforcement Learning Algorithms **

In the realm of academic research, many theories support MARL. In this section, we delve into some of these theories and related algorithms to set the context for our research. 

Deep reinforcement learning \(deep RL\) is a subfield of machine learning that combines reinforcement learning \(RL\) and deep learning \[23\]. Reinforcement learning considers the problem of a computational agent learning to make decisions by trial and error \[23\]. In reinforcement learning, goal-oriented algorithms are designed through trial and error, optimizing for the action that leads to the best result or the action that gains the most “reward” \[24\]. 

Deep RL incorporates deep learning into the solution, allowing agents to make decisions from unstructured input data without manual engineering of the state space \[23\]. Deep RL algorithms can take in very large inputs \(e.g., every pixel rendered to the screen in a video game\) and decide what actions to perform to optimize an objective \(e.g., maximizing the game score\) \[23\]. 

Deep reinforcement learning is typically carried out with one of two different techniques: value-based learning and policy-based learning \[24\]. Value-based learning techniques use algorithms and architectures like convolutional neural networks and Deep-Q Networks \[24\]. Policy-based methods are used when the number of possible actions the agent can take is extremely high, which is typically the case in real-world scenarios \[24\]. 

4 

Q-learning is a traditional reinforcement learning algorithm that can be extended to multiagent settings. 

In Q-Learning, each agent maintains a Q-table that stores the Q-values, representing the expected cumulative rewards for each action in each state. The agents update their Q-values using the Bellman equation and learn to choose actions that maximize their Q-values. Q-learning is simple to implement and can converge to optimal policies in smal -scale environments with few agents. However, it can suffer from scalability issues in large-scale environments due to the exponential growth of the Q-table with the number of states and actions, which makes it computational y expensive. 

Deep Q-Network \(DQN\) is an extension of Q-Learning that uses deep neural networks to approximate the Q-values. Instead of maintaining a Q-table, each agent uses a neural network to estimate the Q-values for its actions. DQNs can handle large-scale environments with continuous state and action spaces and learn complex policies through deep neural networks. However, DQNs suffer from the issue of overestimation, where the Q-values can be overestimated due to using the max operator during action selection, leading to suboptimal policies. Additionally, DQNs may face challenges handling non-stationarity and partial observability in multi-agent environments. Our multi-agent environment is a continuous non-stationary, which does not make this algorithm a favorable choice. 

Advantage Actor-Critic \(A2C\) is a model-based MARL algorithm that combines policy gradient and value function methods. It uses an actor-critic architecture, where the agent maintains a policy \(actor\) and a value function \(critic\). The policy selects actions, while the value function estimates the expected cumulative rewards. A2C can handle large-scale environments with continuous state and action spaces and learn without storing large Q-tables or experiencing replay buffers. It also provides a natural way to handle multiple agents with different policies. However, A2C can have high variance in policy gradients, which can make learning unstable, and it may require careful tuning of hyperparameters \[22\]. The challenges presented by this algorithm can be resolved by fine-tuning the hyperparameters. Hence, the MARL used in this study should be based on the A2C algorithm. In the next section, we will compare MARL 

techniques that can be adopted for this study. 

**2.2. Multi-agent Frameworks **

Multi-agent reinforcement learning \(MARL\) is a sub-field of reinforcement learning that focuses on studying the behavior of multiple learning agents that coexist in a shared environment \[25\]. Each agent is motivated by its rewards and does actions to advance its interests; in some environments, these interests are opposed to the interests of other agents, resulting in complex group dynamics \[25\]. Multi-agent reinforcement learning is closely related to game theory, especially repeated games, and multi-agent systems \[25\]. Its study combines the pursuit of finding ideal algorithms that maximize rewards with a more sociological set of concepts \[25\]. Multi-agent Reinforcement Learning aims to solve complex problems by integrating multiple agents focusing on different sub-tasks. 

According to \[26\], there are two representative frameworks for MARL algorithms: Markov/stochastic games and extensive-form games. These frameworks address different types of tasks in MARL, such as cooperative, competitive, and mixed settings. The cooperative setting involves agents collaborating to optimize a common long-term return, while the competitive setting involves agents whose returns sum up to zero. The mixed setting involves both cooperative and competitive agents, with general sum returns. 

These different settings require frameworks spanning from optimization theory, dynamic programming, game theory, and decentralized control, as discussed \[26\] 

**2.3. Cooperative MARL **

Our research is situated in multi-agent systems working collaboratively to enhance safety and comfort at unregulated intersections. This section delves into various algorithms and theoretical frameworks pertinent to cooperative Multi-Agent Reinforcement Learning \(MARL\). In Cooperative MARL, agents work together to achieve a shared objective. Much of Cooperative MARL involves Homogeneous Agents, meaning agents have a similar shared reward function \[26\]. 

The homogeneity can be identified in Multi-Agent MDP or Markov Teams, where agents have identical Q-functions, and a Q-learning algorithm. However, this doesn’t ensure that the equilibrium policy will converge \[26\]. To address this, coordination is required. Optimal Adaptive Learning \(OAL\) \[26\] is a 5 

significant development in this area, which assures convergence to the equilibrium policy. An important concern in Markov teams is scalability. Some solutions proposed include distributed Q-learning and value function factorization \[26\]. Markov Potential Games, which extend the notion of potential games to sequential decision-making settings, has also been proposed \[26\]. They are like Markov teams and can be analyzed using single-agent RL algorithms. Another proposed solution is the Mean-Field Regime \[26\], which tackles scalability by focusing on many homogeneous agents. This model defines agents’ 

interactions by a mean quantity \(like the average state\). The model simplifies interactions and has been explored in mean field games and team models with mean field sharing \[26\]. Finally, the Decentralized Paradigm with Networked Agents suggests that not all agents are homogeneous. They might have different reward functions but still, cooperate to maximize the team’s average reward \[26\]. Agents can share information with their neighbors over a network if a central controller doesn’t exist. The QD-learning algorithm is a notable development in this domain, which uses consensus and innovation for Q-learning 

\[26\]. 

Another set of models in cooperative settings is characterized by partial observability, a significant challenge for agents \[26\]. While such models are frequent, in-depth theoretical analyses remain sparse. 

These scenarios are often depicted using a decentralized Partially Observable Markov Decision Process \(Dec-POMDP\) \[26\], where agents only view their observations, not their peers, complicating maintaining a global belief state. This complexity categorizes Dec-POMDPs as NEXP-complete \[26\], signifying they are highly time-consuming to resolve. However, there’s a burgeoning interest in developing algorithms for these models, notably through a centralized learning decentralized execution approach \[26\]. In this method, a decentralized problem is transformed into a centralized version, solved centrally using data from all agents, after which policies are distributed to each agent for implementation. Other strategies include streamlining their resolution by converting Dec-POMDPs into different models like non observable MDPs or occupancy-state MDPs \[26\]. Various sampling-based planning/learning algorithms, such as Monte-Carlo sampling and tree search methods, have been introduced to enhance computational efficiency 

\[26\]. Efforts are also underway to bolster decentralized learning in Dec-POMDPs, including techniques that repurpose shared agent observations into a centralized framework, which agents can individually address 

\[27\] \[28\]. 

**2.4. Algorithms in Cooperative MARL **

Consensus Multi-Agent DDPG is a variant of MADDPG that introduces a communication module to enable explicit agent communication. This allows agents to share information about their observations, actions, and intentions, which can improve their coordination and cooperation in complex environments. \[29\] 

QMIX \(Q-value Mixing\) is a centralized MARL algorithm that learns a joint action-value function for all agents by mixing the Q-values of individual agents. It uses a central critic network to estimate the joint action value function and decentralized actor networks for each agent to select actions. QMIX is effective in cooperative tasks, including autonomous vehicle simulations. \[30\] COMA \(Counterfactual Multi-Agent\) is another centralized MARL algorithm that uses counterfactual baselines to estimate the contribution of each agent to the joint action value function. It leverages the concept of counterfactuals to estimate the individual contributions of agents, which allows for more effective coordination and cooperation among agents.\[31\] Team-Deep-Q-Networks \(Team-DQNs\) is a variant of the traditional Deep Q-Network \(DQN\) algorithm that extends it to cooperative MARL. It uses a shared neural network to learn a joint action-value function for all agents and incorporates coordination through a reward-shaping mechanism. Team-DQNs have been applied to cooperative tasks, including autonomous vehicle simulations. \[32\] Multi-Agent Deep Deterministic Policy Gradient \(MADDPG\) extends the original DDPG algorithm for cooperative MARL and has been successfully applied to various domains, including autonomous vehicles. MADDPG allows agents to learn and coordinate their actions cooperatively, enabling them to share information and collaborate to achieve common goals \[22\]. 





6 

**3. Literature Review **

**3.1. History of Autonomous Vehicle **

Autonomous vehicles \(AVs\) have seen considerable development since the United States Defense Advanced Research Projects Agency \(DARPA\) held the inaugural Grand Challenge for AVs in 2004 \[33\]. 

Although it was not the genesis of AVs, the Grand Challenge marked a notable acceleration in the field. 

Previous advancements included exceptional contributions, such as Ernst Dickmanns and his team from the Bundeswehr University of Munich designing a driverless Mercedes-Benz robotic van in the 1980s. This rudimentary AV could achieve 63km/h on traffic-free streets \[33\]. Another remarkable milestone was the Autonomous Land Vehicle \(ALV\) project. Under this initiative, Carnegie Mellon University and associated institutions in the United States developed technology that enabled the first demonstration of road-following at speeds of 31km/h \[34\]. 

Furthermore, Carnegie Mellon University’s Navlab project represented a significant stride toward realizing autonomous navigation. They developed a semi-autonomous vehicle that required human control for braking and throttle but managed to cover 5,000 km, maintaining ful autonomy for an impressive 98.2% 

of the journey \[35\]. These undertakings provided foundational knowledge and established a platform upon which current AV technologies are built. 

However, the recent progress in the industry has galvanized the move toward full autonomy. The fusion of machine learning, robotics, and computer vision research is at the heart of these advancements. It has elevated the capabilities of autonomous vehicles, enhanced their safety and broadened their applicability across various sectors. This integration has facilitated the deployment of AVs in domains such as logistics, transportation, and mobility services, demonstrating the transformative potential of autonomous vehicle technology. 

Today, autonomous vehicles embody an intricate blend of cutting-edge technology and innovative engineering that facilitates efficient, reliable, and safe transportation. As our understanding of AI and machine learning deepens, and computational capabilities continue to improve, we can expect even more sophisticated autonomous systems shortly. This research aims to contribute to this ongoing evolution by exploring novel ways to improve autonomous vehicles’ decision-making process and navigational abilities, particularly in the challenging context of uncontrolled intersections. 

**3.2. Emerging Technologies in AV industry. **

Deep Learning \(DL\), a subset of machine learning, has emerged as a pivotal player in the domain of object detection algorithms \[36\]. Applying DL results in high accuracy and speed and enhances object detection and classification capabilities, which are vital for autonomous vehicles. Autonomous vehicles utilize a variety of sensors to detect and classify objects within their environment. Deep learning allows these vehicles to process the sensor data and make accurate identifications and predictions about the surrounding environment. 

Furthermore, Reinforcement Learning \(RL\), another subset of machine learning, has proven to be incredibly valuable in improving the decision-making capabilities of AVs \[37\]. RL enables autonomous vehicles to learn from their experiences, refining their behaviors and enhancing performance. Researchers have harnessed RL to control critical aspects of autonomous vehicles, such as steering and speed control 

\[38\]. 

The evolution of Multi-Agent Systems \(MAS\) has also significantly impacted the development of autonomous vehicles. By allowing AVs to cooperate and coordinate with each other, MAS have improved the safety and efficiency of autonomous driving, particularly in complex scenarios like intersections and merging lanes \[39\]. The advent of simulation-based testing has been another significant development for AVs. Given that real-world testing can be both costly and time-consuming, simulation-based testing provides a viable alternative that enables researchers to test the behaviors of autonomous vehicles in a virtual environment. This technique allows the detection and correction of issues before deploying cars in the real world \[40\]. 

7 



As autonomous vehicles become increasingly common, understanding how humans interact with them is paramount. Researchers have begun to focus on improving the design of user interfaces and communication strategies to facilitate effective human autonomous vehicle interaction \[40\]. In tandem with technological development, ethical considerations have also emerged. In response, researchers have developed ethical frameworks to guide the behavior of autonomous vehicles and ensure they operate social y responsibly \[41\]. 

The robustness and versatility of AVs are being continually improved upon. For instance, researchers have developed methods to improve the scalability and resilience of autonomous driving systems, such as using multi-sensor fusion and redundancy \[40\]. These developments are bringing us incrementally closer to achieving Level 5 autonomy. The Society of Automotive Engineers \(SAE\) International \[42\] \[40\] defines six levels of autonomy based on a vehicle’s capability to operate without human intervention: 1. Level 0: No Automation - No autonomous technology is involved; the driver is entirely responsible for driving. 

2. Level 1: Driver Assistance - Vehicle features such as adaptive cruise control or lane keeping assistance assist the driver in specific situations. 

3. 

Level 2: Partial Automation - Two or more automated functions work synergistical y, but the driver must remain engaged and ready to take control. 

4. Level 3: Conditional Automation - The vehicle can autonomously handle certain situations but will request the driver to take over when needed. 

5. Level 4: High Automation - Autonomous operation covers most driving situations, though human intervention may be needed under extreme conditions. 

6. Level 5: Full Automation - The vehicle operates autonomously under all situations and conditions, requiring no human intervention. 



In recent years, substantial progress has been made toward achieving levels 2 to 5. Level 2 systems have become common in production vehicles, and Level 3 systems are under testing in select vehicles. 

Meanwhile, the development of Level 4 and Level 5 systems continues to progress and are expected to be deployed in the forthcoming years \[41\]. Nevertheless, many technical, legal, and societal challenges must be addressed before fully autonomous vehicles become commonplace \[41\]. In the context of this research, we aim to make a meaningful contribution to the advancement of AVs by enabling them to navigate complex environments such as intersections more effectively. 

**3.3. Intersection and Autonomous Vehicles **



*Figure 2. Different types of intersections *

Intersections pose a significant challenge to the progress of AVs, constituting one of the most complex environments for these vehicles to navigate successfully. The dynamic nature of intersections \(See Figure 2\), where cars, pedestrians, and diverse traffic rules converge, necessitates that AVs have sophisticated 8 

detection and response capabilities \[43\]. As stated by Bhatt et al. \[43\], AVs must not only be able to detect intersections but also classify them based on their type, such as four-way, T-shaped, and roundabouts \(See Figure 2\), while identifying applicable traffic rules, regardless of whether the intersections are controlled or uncontrolled. 

The AVs utilize an ensemble of sensors, including Light Detection and Ranging \(LiDAR\), cameras, and radar, to gather comprehensive environmental data. In line with \[44\], an autonomous vehicle must effectively detect and track other vehicles within the intersection, registering their speed, direction, and potential actions. This feat is accomplished using computer vision algorithms, machine learning, and sensor fusion, empowering the "ego" vehicle \(the vehicle with the agent in focus\) with the predictive capability necessary for preemptive safety measures. 

In addition, an AV must accurately detect and track pedestrians, including their position, movement, and intentions to safely navigate intersections. Like vehicle detection, this task is achieved using computer vision algorithms and sensor fusion \[45\]. Moreover, traffic signals, including stop signs, yield signs, and traffic lights, must be recognized by AVs, which is a task often addressed using computer vision algorithms and machine learning \[46\]. Once the vehicle successfully perceives its surroundings, it must effectively traverse the intersection while considering other road users’ behavior. Advanced planning and decision-making algorithms are critical in this step, promoting efficient and safe navigation \[47\]. 

The goal of achieving Level 5 autonomy necessitates that AVs master navigation through intersections, thereby minimizing the risk of accidents and collisions \[48\]. This advancement also raises the complex issue of liability and responsibility in case of an accident, further highlighting the intricacies associated with autonomous navigation. The development of autonomous vehicles capable of safely and efficiently navigating intersections is a complex ongoing research subject, with several challenges, such as sensor reliability, robustness to environmental conditions, and ethical considerations, yet to be fully addressed. 

In this research, we delve into the complexities and chal enges of intersections, focusing on facilitating cooperation among AVs during navigation. This exploration will provide valuable insights and advancements, contributing to the broader pursuit of Level 5 autonomy. 

**3.4. Safety and Comfort Decision-Making in Autonomous Vehicles **

Autonomous Vehicles \(AVs\) are on the brink of transforming the global transportation system. A critical aspect of their widespread acceptance lies in the capability to make decisions that ensure safety and comfort for passengers and other road users. The notion of AV cognition, particularly automatic decision-making in autonomous vehicles, is a crucial aspect that significantly impacts the development and deployment of AVs operating at Level 5 autonomy. \[49\]. 

Safety is paramount in the realm of autonomous driving. A major driver behind the push for AVs has been the potential to reduce road accidents significantly, with many attributing most road mishaps to human error \[50\]\[51\]. Machine learning models, especially deep learning and reinforcement learning have shown promise in training AVs to navigate complex traffic scenarios and ensure safety \[52\]\[53\]. Recognizing the behaviors and intents of surrounding entities, like pedestrians and other vehicles, is vital for safe decision-making. Current systems employ sensor fusion, which combines data from LIDARs, radars, and cameras to build a robust environmental perception \[54\]. Once the environment is understood, evaluating risks associated with different driving decisions becomes crucial. Techniques like probabilistic modeling and Bayesian networks have been explored to predict and quantify risks \[55\]. Decision-making algorithms have been designed to determine the most suitable actions based on risk assessments. Model Predictive Control \(MPC\) and potential field methods are popular techniques for this \[56\]. 

S. Raul and his team, in their paper \[57\], put forth an ecological perspective toward developing digital environments for the training of AVs. They emphasize that the driving agent should be viewed as interacting within an increasingly intricate environment, particularly while navigating complex road situations such as roundabouts and intersections. 

Raul et al. argue that new theories catering to decision-making and social coordination must be proposed, as AVs are anticipated to share the roads with human-driven vehicles \(HDVs\). This coexistence demands that AV training incorporates cognitive theories, enabling them to operate at human cognition levels, thereby enhancing road safety and cooperation \[57\]. They propose utilizing concepts from interpersonal coordination and decision-making in sports for the cognitive training of AVs. This approach aims to allow 9 

the AV’s driving agent to harness affordances provided by technology and human drivers in the environment, thereby enhancing driving perception \[57\]. This opens new research opportunities to delve into the significance of human-level cognition in AVs. In this thesis, we explore this direction, focusing on fundamental levels of cognitive training for AVs to detect oncoming vehicles at the intersection and take necessary actions to prevent collisions. 

The idea of AV cognition is also embraced in the work of Driggs-Campbell et al., titled 

"Integrating intuitive driver models in autonomous planning for interactive maneuvers" \[49\]. The authors acknowledge the impending reality of AVs being deployed on roads, sharing space with HDVs. They argue that for AVs to navigate in such a mixed environment safely and comfortably, they must develop a "shared mental model." This model should encapsulate nuanced road interactions and precise collaborative maneuvers modeled on those practiced by human drivers \[49\]. 

The proposed shared mental model bridges AVs and HDVs, providing a framework for understanding and predicting each other’s behavior. As a result, AVs can then be equipped to mimic the intuitive decision-making process of human drivers, adapting, and responding to changes in real-time, much like their human counterparts. This approach ensures safety and facilitates smoother integration of AVs into the existing traffic ecosystem, reinforcing the importance of considering human-like cognitive abilities and intuitive decision-making in the development and deployment of Avs. 

While safety remains a primary concern, the comfort of passengers inside AVs is also pivotal. An autonomously driven car that constantly brakes or accelerates abruptly might be perceived as uncomfortable, even if technically safe. Jerky motions, sudden stops, or sharp turns can be discomforting. 

Research indicates that using smoother trajectory planning algorithms can mitigate such issues \[58\]. 

Giving passengers insights into the vehicle’s decision-making process, possibly through intuitive interfaces, can enhance trust and perceived comfort \[59\]. Anticipating and avoiding scenarios that might cause stress to passengers, such as aggressive merging or too-close tailgating, is an area of active research. 

This goes beyond physical comfort, addressing the mental well-being of the vehicle’s occupants. 

Despite advancements, challenges persist. One key challenge is the decision-making in mixed-traffic scenarios, where AVs share the road with human-driven vehicles. The unpredictable nature of human drivers introduces complexities in decision-making algorithms \[60\]. Moreover, ensuring comfort while not compromising on safety is a delicate balance that remains an ongoing area of research. Another challenge is the generalizability of algorithms across diverse scenarios and cultural contexts. Driving norms and what’s perceived as "comfortable" can vary across regions, demanding more adaptable algorithms \[61\]. 

The journey of AVs towards widespread acceptance is closely linked with their ability to ensure safety and comfort. While significant strides have been made, there’s still an academic and practical journey to perfect these systems. Addressing the highlighted challenges will be crucial for the next phase of AV development. 

Integrating human-like cognition and involuntary decision-making in AV training represents a promising avenue toward ensuring the smooth coexistence of level 5 autonomous AVs and HDVs on the roads. 

**3.5. Reinforcement Learning** 

Reinforcement Learning \(RL\), a subset of machine learning, presents a promising methodology to tackle the complexity of navigation tasks that AVs encounter, particularly at intersections. Rooted in the principle of decision-making through trial and error, RL equips an agent to interact with an environment, make actions, and receive rewards based on these actions \[62\]. The agent aims to maximize the cumulative reward over time by learning a policy that effectively maps states to actions, thus mimicking a form of intuition \[62\]. 

This intuitive decision-making, facilitated by RL, has found successful applications in many fields, including robotics, gaming, recommendation systems, and, most notably, autonomous driving. RL algorithms can be classified into value-based, policy-based, and model-based methods \[63\]. Value-based strategies focus on learning an estimate of the state-value or action-value functions to derive an optimal policy. In contrast, policy-based methods directly learn the policy without estimating value functions. On the other hand, model-based methods focus on understanding the environment’s dynamics to plan and execute actions 

\[63\]. 

In recent years, Deep Reinforcement Learning \(DRL\) has emerged as a powerful approach to handling complex RL problems that necessitate high-dimensional state and action spaces. It utilizes deep neural 10 



networks to approximate the value function or policy, enabling the agent to learn from high-dimensional sensory inputs such as images and speech \[63\]. This ability of DRL algorithms to handle high-dimensional data is particularly relevant for AVs that rely heavily on rich sensory input for navigation. 

Recent advancements in RL have improved RL algorithms’ sample efficiency and stability and led to the development of innovative techniques like Multi-Agent RL \(MARL\) \[29\]. MARL extends the application of RL to scenarios where multiple agents interact with each other and the environment, which is crucial in autonomous driving at intersections, where numerous vehicles need to coordinate their actions. It has found successful applications in cooperative control of autonomous vehicles, robotic systems, and traffic control \[22\] \[64\] \[65\] \[66\]. 

Meta-learning, another innovative use of RL, focuses on learning how to learn. Meta-learning algorithms 

\[67\] draw from experiences across multiple tasks to quickly adapt to new ones. This concept has significant potential for AVs operating in dynamic environments like intersections, as it allows for rapid adaptation to novel scenarios. Meta-learning has been applied to diverse problems, including few-shot learning, hyperparameter optimization, and robotics \[67\]. 

The sophistication and adaptability of RL and its variants, such as DRL, MARL, and meta-learning, offer an excellent set of tools for AVs to navigate the challenges posed by intersections. By applying these techniques, AVs can be equipped with a level of ’intuition,’ enabling them to make optimal decisions in complex, dynamic environments, thus pushing us closer to achieving Level 5 autonomy. 

**3.6. Multi Agent Reinforcement Learning \(MARL\) **

The prior discussion on applying Multi-Agent Reinforcement Learning \(MARL\) to Autonomous Vehicles \(AVs\) highlights its potential for handling complex navigational tasks through decentralization, cooperation, and competition. Notably, this paradigm integrates intuitive decision-making into the navigation of AVs, providing a unique avenue to explore further. 





*Figure 3. Multi agent reinforcement learning *

MARL forms an essential part of artificial intelligence \(AI\) research, focusing on developing intelligent agents capable of learning and interacting within a dynamic environment \[68\]. This learning paradigm applies to autonomous driving as vehicles navigate shared environments, interacting with and responding to other road users’ behaviors. By optimizing individual objective functions, each ’agent’—in this context, an AV—can navigate its environment efficiently and safely. 

MARL algorithms, either centralized or decentralized \(See Figure 3\), define the scope of interaction and learning among agents \[68\] \[69\]. A centralized approach assumes a central controller coordinates the actions of all agents. Conversely, a decentralized approach allows agents to learn to coordinate their actions independently. This decentralized approach aligns more closely with intuitive decision-making, where AVs must react and adapt to their environments independently. 

Several algorithms have been developed to optimize MARL, including Q-learning, policy gradient methods, actor-critic methods, and deep reinforcement learning \(DRL\) \[68\]. The strength of DRL, especially in managing high-dimensional state spaces and nonlinear policies, led to the successful application of deep 11 

multi-agent reinforcement learning \(DMARL\), which uses deep neural networks to represent the policies of multiple agents \[31\] \[70\]. 

Further, MARL’s cooperative, competitive, and mixed types find applicability across many domains. In cooperative MARL, agents work together towards a shared goal—an essential strategy for autonomous driving where vehicles must collaborate to ensure smooth traffic flow. This has been proven effective in diverse scenarios, such as coordinating unmanned aerial vehicles \(UAVs\) \[71\], managing traffic \[72\], and even enabling robots to perform tasks cooperatively \[66\]. 

Alternatively, competitive MARL applies when agents strive to optimize their objectives—an approach that could apply to scenarios where AVs compete for resources like charging spots. This competitive approach has yielded superior performance in areas such as gaming \[64\] and optimizing travel time in traffic control 

\[73\]. 

Mixed MARL integrates elements of cooperation and competition, allowing agents to switch their behavior based on the task at hand—a valuable approach for AVs, given their operating environments’ dynamic and often unpredictable nature. This approach has proven advantageous in financial portfolio management 

\[74\] and robotics \[29\], indicating a potential for application in AV navigation. 

The discussion thus far has underlined the importance of Multi-Agent Reinforcement Learning \(MARL\) in advancing the field of autonomous vehicles \(AVs\), particularly in facilitating cooperative control to optimize traffic flow, reduce congestion, and avoid collisions. The success of MARL in this context draws heavily from its ability to allow multiple AVs, viewed as agents, to coordinate their actions and adapt to their shared environment. 

This application of MARL in the context of AVs extends to various specific situations. For instance, \[73\] 

utilized deep reinforcement learning, a subclass of MARL, to guide multiple AVs in coordinating their actions to prevent accidents. This is particularly relevant in AV navigation as it encompasses the intuitive decision-making that comes into play when multiple vehicles negotiate for space on the road, avoiding collisions in real time. 

Similarly, MARL has been instrumental in optimizing traffic control systems in bustling urban areas. In one study, \[65\] successfully implemented MARL to develop an adaptive traffic signal control system capable of adjusting to fluctuating traffic conditions to curb congestion. The adaptability of MARL presents a novel approach to managing intersections, an infamously complicated task given the interplay of multiple vehicles simultaneously. 

The concept of cooperative driving, where multiple AVs coordinate their actions towards common goals such as col ision avoidance and congestion reduction, has also benefited from MARL. This was demonstrated in a study by \[75\] where they applied a MARL approach to learn a coordination policy for a platoon of AVs. Each vehicle acted as an independent agent, sharing state information with neighboring cars. The study revealed that this multi-agent approach surpassed a single-agent system regarding reduced travel time and fuel consumption. 

Intersection management, a critical task for AVs, has also seen the benefits of implementing MARL. In research by \[76\], a policy for managing AVs at a four-way intersection was developed using MARL. The resultant MARL approach outperformed a fixed time signal approach by minimizing waiting time and increasing throughput. 

Traffic control, another critical task for AVs involving the management of traffic flow and congestion reduction, has witnessed the successful application of MARL as well. A study by \[32\] employed MARL to learn a policy for managing traffic at roundabouts, with results showing improved travel time and reduced queue length compared to fixed-time signal methods. 

The practice of platooning, where a group of AVs closely follow each other in a single lane to boost fuel efficiency and mitigate congestion, has seen MARL application too. \[77\] used a MARL approach to develop a platooning policy for a group of AVs on a highway. This MARL approach demonstrated superior performance over single-agent methods regarding reduced fuel consumption and improved stability. 

Considering these examples, MARL’s broad applicability and demonstrated success in AV research is evident. As we strive to unravel intersection challenges for AVs, the utility of MARL becomes ever more apparent. This proposition is further supported by work conducted by \[22\], making MARL a fitting technique for our exploration. This integration of MARL into AV navigation allows us to tackle complex, real-world traffic scenarios, thereby enhancing AVs’ safety, efficiency, and reliability in our shared spaces. 

12 

MARL provides a robust framework for incorporating intuitive decision-making into the operation of AVs. 

By building on the principles of MARL and tailoring them to specific navigational challenges, such as intersection navigation, we can enhance AVs’ safety, efficiency, and reliability in real-world environments. 

**3.7. Overview of Simulators **

Autonomous simulators are crucial for developing and testing autonomous vehicles in a safe and controlled environment. High-fidelity simulators provide a realistic and immersive experience that allows researchers and developers to test and refine autonomous systems before they are deployed on real-world roads. In this section, we provide an overview of three of the high-fidelity simulators for AVs. 

SUMO \(Simulation of Urban Mobility\) is an open-source microscopic traffic simulator widely used in academic research \[78\] for modeling and simulating transportation systems. It provides a high-fidelity environment for testing and developing autonomous driving algorithms. The simulator supports various sensors, including cameras and lidars, and provides a rich set of APIs for developing and testing custom autonomous driving algorithms. This \[79\] work evaluated the effects of different vehicle platooning strategies on traffic flow performance and fuel consumption using SUMO simulations. The results showed that cooperative adaptive cruise control \(CACC\) and cooperative lane change \(CLC\) could significantly improve traffic flow efficiency and reduce fuel consumption \[79\]. In another work \[79\], the authors provided a comprehensive survey of integrating connected and automated vehicles \(CAVs\) into traffic simulations, including a discussion of SUMO. The authors discussed the chal enges and opportunities of integrating CAVs into SUMO simulations and presented several existing approaches for doing so \[79\]. In this work, SUMO was used to model emergency medical services \(EMS\) in an urban area in Indonesia. The study demonstrated the feasibility of using SUMO to model complex transportation systems, such as EMS, and provided insights for improving the efficiency of EMS in urban areas \[80\]. Our review of the tool shows that it is suitable for ITS, which is one reason we did not adopt it in this research. The other reason is that we did not find the tool user-friendly. 

AirSim is an open-source, cross-platform simulator for drones, cars, and more, built on Unreal Engine and designed by Microsoft. It provides a realistic environment for testing and developing various autonomous systems and AI algorithms \[81\]. AirSim provides a real simulation environment that includes physics-based models of the vehicle, the environment, and the sensors. It considers various factors such as gravity, wind, and ground friction \[82\]. AirSim allows the simulation of multiple sensors like cameras, lidars, and radars. It generates realistic sensor data that can be used for testing and developing various algorithms 

\[81\]. AirSim allows you to create customized environments, including real-world locations. You can add your objects and structures to the environment. AirSim can run on Windows, Linux, and macOS. AirSim is open-source, and its source code is available on GitHub. This means that developers can customize and extend the simulator per their requirements. AirSim is compatible with machine learning and AI platforms such as TensorFlow, Keras, and PyTorch. This makes it easy to develop and test AI algorithms. Sadhu et al. 

\[83\] proposed a method for Simultaneous Localization and Mapping \(SLAM\) using neural networks and external memory. The method was tested on the AirSim platform with a simulated quadrotor and achieved state-of-the-art performance \[83\]. Nagami et al. \[84\] also proposed a method for reinforcement learning that utilized a model-based approach with demonstrations. The method was tested on the AirSim platform with a simulated car and achieved superior performance compared to existing methods \[84\]. After reviewing this simulator, a few reasons did not make it suitable for our thesis. Getting AirSim up and running can be complex, especially for those without a background in software development or familiarity with Unreal Engine. Unreal Engine, on which AirSim is built, is a high-end game engine that requires significant processing power and memory. Currently, AirSim primarily supports models for quadrotor drones and a limited model of ground vehicles. 

CARLA is an open-source autonomous driving simulator that provides a high-fidelity urban environment for testing and validating autonomous driving algorithms \[85\]. CARLA has been widely used in academia and industry for research, development, and testing of autonomous vehicles. The simulator supports various sensors, including cameras, lidars, and radars, and provides a flexible API for developing and testing custom autonomous driving algorithms \[85\]. Wang et al. provided a comprehensive survey of human-robot interaction \(HRI\) in autonomous driving, including a discussion of CARLA. The authors discussed the benefits of using CARLA for evaluating HRI strategies and developing human-aware autonomous driving algorithms \[86\]. Sistu et al. \[87\] proposed a real-time joint detection and 13 

segmentation method for autonomous driving on unstructured roads. The method was evaluated on the CARLA simulator and achieved promising results \[87\]. We adopted this simulator because of our familiarity with this tool. We also find this tool much more user-friendly, which is the other reason why we chose this tool over AirSim, although we are familiar with AirSim. 





14 



**4. Research Methodology **

**4.1. Design Science **

Design science has been applied in various domains, including information systems, healthcare, engineering, and management. It has been used to develop innovative solutions, such as decision support systems, medical devices, and sustainable technologies. Design science is a valuable research paradigm for several reasons, supported by various studies and articles. Design science is focused on developing innovative solutions to practical problems. By using design science, researchers can create artifacts that address specific issues in real-world contexts. This can lead to more effective and valuable solutions compared to other research paradigms that focus solely on theory \[88\]. Design science research is relevant and applicable to various domains, including information systems, healthcare, engineering, and management. This makes it a versatile research paradigm that can be applied to many problems \[89\]. 

Design science research follows a thorough and systematic process that involves identifying a problem, setting objectives, designing, and developing an artifact, demonstrating its effectiveness, and evaluating the design process. This ensures the research is well-planned and executed, leading to reliable and valid results \[90\]. Design science research can also contribute to theory by developing new models, methods, and algorithms that can be used to solve similar problems in the future. This can lead to advancements in the field and help to build a body of knowledge. One of the seminal works in design science is by Peffers et al. \[91\], which outlines the fundamental principles and processes of design science research. According to them, design science research involves the following steps, as shown in Figure 4: 1. Problem identification and motivation: identifying a problem, opportunity, or phenomenon that requires a solution. 

2. Objectives of a solution: the objectives included consistency with DS processes in prior literature, the development of a nominal process for conducting research, and the development of a mental model for DS research output. 

3. Design and development: design and develop artifacts/solutions to address the identified problem. 

4. Demonstration: validate if the designed artifacts address the identified problem. 

5. Evaluation: evaluating the artifact and the design process to identify strengths, weaknesses, and opportunities for improvement. 

6. Communication: communicate the significance of the problem, the artifacts, and how it addresses the problem. Communicates also the entire research process \[91\]. \[92\]. 





*Figure 4. Design Science research process \(DSRP\) model *

Design science research is a problem-solving paradigm that seeks to enhance human knowledge through the creation of innovative artifacts \[93\]. It is a rigorous methodology that involves developing and 15 

performing designed artifacts to improve functional performance. Design science research focuses on creating prescriptive knowledge, explaining why artifacts enhance or disrupt their relevant application contexts. As a research methodology, design science stands distinct from several other methodologies and approaches, including but not limited to action research, grounded theory, case studies, prototyping, and experimentation. While each approach has its merits and specific application areas, our choice of design science over others, especially prototyping and experimentation, is grounded in several key considerations. 

Prototyping, for instance, primarily focuses on developing preliminary versions of solutions to gauge their feasibility or understand user requirements better \[94\]. While it’s an invaluable tool for iterative development and refinement, prototyping does not always emphasize the foundational theoretical underpinnings that guide the creation of the solution. It may often focus on the ’how’ without deeply considering the ’why.’ 

Experimentation, on the other hand, emphasizes testing hypotheses under controlled conditions. It is instrumental in establishing causal relationships and understanding the effects of specific interventions. 

However, experimentation, especially in isolation, might miss out on the holistic design and development process, which deeply considers both the problem and the solution space \[95\]. 

In contrast, design science amalgamates the strengths of these approaches. It encourages the development of innovative solutions \(akin to prototyping\) and ensures that these solutions are grounded in rigorous theoretical frameworks. Design science does not stop at creating a prototype; it emphasizes understanding the problem in depth, designing a relevant solution, and validating that solution, often through methods that include experimentation. Moreover, the iterative nature of design science, which involves refining the artifact based on feedback and evaluation, mirrors the iterative benefits of prototyping \[96\] \[95\]. 

Furthermore, while experimentation gives us ’what’ is happening and ’to what extent,’ design science often provides the ’why’ and ’how’ - the deeper understanding essential when crafting solutions for complex problems, such as the challenges faced by AVs at intersections. 

For our research on AVs, the intricacies of intersection navigation demand an approach that doesn’t just offer a solution but ensures this solution is theoretically sound, practically relevant, and validated in real-world or close-to-real-world contexts. Given this, design science emerges as a more comprehensive approach than mere prototyping or isolated experimentation. 

Moreover, given the rapid technological advancements in areas like AVs, research paradigms that can swiftly turn challenges into tested solutions are paramount. For our research on AVs, navigating intersections requires a holistic solution-oriented approach that design science is uniquely positioned to offer. Hence, our choice of design science for developing a MARL solution for AVs is rooted in its holistic, rigorous, and solution-driven nature. We believe this will yield a tangible artifact to address the AV 

challenge and contribute to MARL’s broader theoretical understanding and application in complex real-world scenarios. 

**4.2. Application of design science in this research **

We have sectioned the paper in the design science methodology context in the following way. Section 2 

delineates the problem statement, focusing specifically on problem identification. It sets the groundwork for a comprehensive understanding of the problem domain. Section 1 presents the proposed solution, contextualizes it with a literature review in Section 3, and elucidates the underlying motivation for this solution. Section 4 Corresponds to the third step in the design science framework, this section offers a detailed exposition of the design and implementation aspects. Section 5 aligns with the fourth step of the design science approach, wherein we illustrate the artifact. It specifically elaborates on the simulation environment and the training regimen for the MARL. Section 6 focuses on demonstration of the artifact. 

Sections 7, 8 and 9 is dedicated to evaluation, adhering to the evaluation step in the design science paradigm. Section 10 furnishes a comprehensive communication of the research trajectory and can be perceived as an encapsulation of the entire research endeavor. 





16 



**5. Design and Implementation **

**5.1. Deep Deterministic Policy Gradient Algorithm** 

We provide some mathematical theory behind our chosen algorithm for MARL \(Cooperative MADDPG\). 

The Deep Deterministic Policy Gradient \(DDPG\) belongs to the categories of MARL described as 

"Centralized Planned, Decentralized Execution." It is a model-free, off-policy reinforcement learning algorithm that combines deep neural networks with deterministic policy gradients to learn policies for continuous action spaces, as we set up in this thesis. DDPG is based on the framework of MDPs, which consists of a tuple \( *S*, *A*, *P*, *R*\), where: *S * is the state space representing the possible states of the environment. 

*A * is the action space representing the possible actions that an agent can take. *P * is the state transition probability function \[22\], which specifies the probability of transitioning from one state to another given a particular action. *R * is the reward function, which provides feedback to the agent by assigning a scalar value to each state action pair, indicating the immediate reward obtained. 

DDPG uses a deterministic policy denoted by µ\( *s*|θ\), where *s * is the state and θ represents the policy parameters. The policy maps states to deterministic actions in the action space. DDPG uses two neural networks, commonly referred to as the actor and critic networks: \(i\) Actor-network is responsible for learning the policy µ\( *s*|θ\) and is trained to maximize the expected cumulative reward. It takes the current state *s * as input and produces an action *a * using the deterministic policy µ\( *s*|θ\). \(ii\) The critic-network estimates the action-value function *Q*\( *s*, *a*\) and is trained to approximate the optimal action-value function. 

It inputs the current state *s * and action *a * and outputs the estimated action value *Q*\( *s*, *a*\). 

DDPG uses the Bellman equation, a fundamental equation in reinforcement learning, to update the critic network. The Bellman equation expresses the action-value function in terms of the immediate reward and the expected future action-value represented in the equation below. 

*Q*\( *s*, *a*\) = *R*\( *s*, *a*\) \+ γ \* *Q*′\( *s*′,µ\( *s*′|θ′\)\), Where *R*\( *s*, *a*\) is the immediate reward, γ is the discount factor, *s*′ is the next state after taking action *a*, µ\( *s*′|θ′\) is the action selected by the target actor-network, and *Q*′\( *s*′,µ\( *s*′|θ′\)\) is the estimated action-value of the next state and the action selected by the target actor-network. 

DDPG uses stochastic gradient descent \(SGD\) to update the actor and critic-networks. The actor-network is updated to maximize the estimated action-value *Q*\( *s*, *a*\) obtained from the critic-network. The critic-network is updated using the mean squared error \(MSE\) loss between the estimated action value *Q*\( *s*, *a*\) and the target value computed using the Bellman equation. 

DDPG employs an experience replay buffer to store past experiences \( *s*, *a*, *r*, *s*′\) observed during interactions with the environment. The buffer samples batches of experiences for training the actor and critic networks. 

This helps to improve the stability of the learning process by decorating the sequential experiences and allowing for efficient reuse of past experiences. 

DDPG uses target networks to stabilize the learning process. The target actor-network is a copy of the actor network with delayed updates, and the target critic-network is a copy of the critic-network with delayed updates. These target networks are used to compute the target action and target value in the Bellman equation during training, providing a more stable target for learning. 

17 



**5.2. Multi-agent Deep Deterministic Policy Gradient** 



*Figure 5. MADDPG Architecture *

Multi-Agent Deep Deterministic Policy Gradient \(MADDPG\) extends the DDPG algorithm to scenarios with multiple agents, as shown, where each agent interacts with its environment and learns a deterministic policy. The main difference between MADDPG and DDPG is the consideration of multiple agents and their interactions \(See Figure 5\). To design Cooperative MARL, we first create MADDPG, which we extend to the Cooperative MADDPG. 

In our Multi-Agent setting, multiple agents are denoted by *i *= 1, 2, .., *N*, where *N * is the total number of agents. Each agent *i * interacts with its environment observes its state *si*, takes its action *ai*, and receives its reward *ri*. The agents perform joint actions by perceiving information from their environment. We modelled the agents’ deterministic policies, denoted by µ *i*\( *si*|θ *i*\), where θ *i * represents the policy parameters for agent *i*. The policies map the individual agent’s state to its deterministic action. The joint action for all agents is denoted by *a *= \( *a* 1, *a* 2, ..., *aN*\), where *ai * is the action taken by agent *i*. 

We use a critic-network for each agent to estimate the action value function *Q*\( *s*, *a*\) for each agent. The critic-network for agent *i * takes the joint state *s * and joint action *a * as input and outputs the estimated action value *Q*\( *si*, *a*\). Each agent’s critic network is trained to approximate the optimal action-value function for that agent. Then, we use the Bellman equation like DDPG but extended for the multi-agent setting. The Bellman equation expresses the action-value function for each agent in terms of the immediate rewards and the expected future action values: 

* Q*\( *si*, *a*\) = *ri *\+ γ \* *Q*′\( *s*′ *i*, *a*′\), Where *ri * is the immediate reward for agent *i*, γ is the discount factor, *s*′ *i * is the next state after taking the joint action *a*, *a*′ is the joint action selected by the target actor-networks and *Q*′\( *s*′ *i*, *a*′\) is the estimated action-value of the next state and the joint action selected by the target actor-networks. 

To update policies, we use stochastic gradient descent \(SGD\) to update each agent’s actor and critic networks. The actor-networks are updated to maximize the estimated action-value *Q*\( *si*, *a*\) obtained from the critic-networks. The critic-networks are updated using the mean squared error \(MSE\) loss between the estimated action value *Q*\( *si*, *a*\) and the target value computed using the Bellman equation. Like DDPG 

and all MADDPG, we employ an experience replay buffer to store each agent’s past experiences \( *s*, *a*, *r*, *s*′\). 

However, in our variation of the MADDPG, we implement a global relay buffer to store past experiences of all agents. 

𝑛𝑛

�\(s, a, r\)𝑠𝑠′\) 

𝑖𝑖=0

Experiences are randomly sampled from the replay buffer during training to break temporal correlations and improve the stability of the learning process. 

18 

**5.2. Cooperative MADDPG Policy for Global Shared Experience Buffer** Since we aim to ensure that agents cooperate at the intersection, we must extend the above MADDPG model to focus on cooperative scenarios. Cooperative Multi-Agent Deep Deterministic Policy Gradient \(Cooperative MADDPG\) is a variant of the MADDPG algorithm that focuses on cooperative scenarios where multiple agents work together towards a common goal. The mathematical framework of cooperative MADDPG is similar to that of MADDPG, with additional considerations for cooperative interactions. 

Joint Reward: In Cooperative MADDPG, we introduce a joint reward. The agents receive a joint reward, denoted by *R*, which represents the shared reward signal that reflects the performance of all agents together. The joint reward is typically designed to incentivize cooperative behavior, where the agents need to collaborate and coordinate their actions to achieve the common goal \[70\]. 

Decentralized Policy, Centralized Value: In the Cooperative MADDPG, we model the agents to have still individual policies, denoted by µ *i*\( *si*|θ *i*\), where θ *i * represents the policy parameters for agent *i*. However, critics \(value functions\) are trained central y, considering all agents’ joint actions and states. This means that each agent has its policy that it follows during execution, but during training, the critics consider the joint actions of all agents to compute the action-value function \[29\]. 

Centralized Critics: In the Cooperative MADDPG, we use centralized critics to estimate the joint action-value function *Q*\( *s*, *a*\), where *s * is the joint state and *a * is the joint action. The centralized critics take the joint state *s * and joint action *a * as input and output the estimated joint action-value *Q*\( *s*, *a*\). The critics are trained to approximate the optimal joint action-value function that reflects the coordination and cooperation among the agents \[29\]. 

Bellman Equation: We used the Bellman equation in Cooperative MADDPG to consider the joint reward. 

The Bellman equation expresses the joint action-value function *Q*\( *s*, *a*\) in terms of the joint reward *R*, the immediate rewards for each agent, the next joint state 

*s*′, and the next joint action *a*′: 

𝑄𝑄\(𝑠𝑠, 𝑎𝑎\) = 𝑅𝑅 \+ ∑𝑁𝑁

′

𝑖𝑖 \(𝛾𝛾 ∗ 𝑟𝑟𝑖𝑖 \) \+ 𝛾𝛾 ∗ 𝑄𝑄′\(𝑠𝑠′, 𝛼𝛼′\). 

Where *ri*’ is the immediate reward for agent *i * in the next time step, γ is the discount factor, *s*′ is the next joint state, *a*′ is the joint action selected by the target actor networks, and *Q*′\( *s*′, *a*′\) is the estimated joint action value of the next state and the joint action selected by the target actor networks. 

The variance in the Cooperative MADDPG versus updated rules for MADDPG is the addition of the joint reward. The actor networks are updated to maximize the estimated joint action-value *Q*\( *s*, *a*\) obtained from the centralized critics, and the critics are updated using the mean squared error \(MSE\) loss between the estimated joint action-value *Q*\( *s*, *a*\) and the target value computed using the Bellman equation. \[29\]. 

**5.3. Learning Policy **

The learning policy includes these specific observation spaces, action spaces, and rewards learnable by the AVs. Observation space is the information each Av collects from its environment. 

1. RGB camera images from each AV’s forward-facing camera. The RGB camera collects images of the AV’s surroundings. The raw data is passed through a ResNet to extract features such as obstacles on the road, whether the intersection is signalized or not, and other road signage and road markings. 

These features become part of the state representation of the AV for effective learning. 

2. Relative positions, velocities, and orientations of nearby vehicles for each AV. 

Action space consists of the actions that Each AV can take based on its perception of the environment. 

1. Throttle: Continuous control for acceleration, ranging from 0 to 1 for each AV. 

2. Brake: Continuous control for deceleration, ranging from 0 to 1 for each AV. 



**5.4. Rewards Definition **

A reward is given to each AV based on its actions and its state. This reward function encourages the AVs to drive smoothly. This is ensured by penalizing the agent for overaccelerating, unnecessarily stopping, and/or going outside its lane. The reward system also encourages the agent to comply with traffic rules. 

The vehicle receives penalties for each traffic rule it violates, including failing to yield, stopping 19 



unnecessarily, or violating priority rules - yield when necessary and avoids collisions. It receives a reward if the vehicle successfully yields when it’s supposed to. If the vehicle collides with another object, it receives a significant penalty. These behaviors are all essential for safe and efficient driving. By assigning rewards and penalties for these behaviors, the reward function helps guide the agents’ learning process, encouraging them to learn policies that maximize their total reward over time. Each agent receives compensation for its contribution to the safety of the intersection. And contribute to the cumulative rewards for all AVs. 

1. \+5 for each AV that successfully crosses the intersection without collisions. 

2. -10 for each AV that col ides with other vehicles or obstacles. 

3. -1 for going outside lane. 

4. -1 for excessive acceleration or deceleration for each AV. 

5. \+5 for each AV that yields to the right and allows other AVs to cross. 

6. -5 for each AV that violates the priority to the right rule and causes collisions. 

**5.5. The Simulated Environment** 

Figure 6 is the architecture of the local experience MADDPG, and Figure 7 shows the globally shared experience MADDPG. Figure 8 shows a detail flow chart of the internal architecture of how agents contribute towards the joint reward. The “CarlaEnvironmentWrapper” class is a key component for interfacing with the Carla driving simulator, facilitating the application of the multi-agent deep deterministic policy gradient \(MADDPG\) algorithm. The class initializes and controls the simulation environment, handling the execution of actions and computation of rewards. It also monitors the termination conditions of each episode, which could be a vehicle reaching its destination or hitting the maximum step count of 1000 per episode. One of its critical roles is in processing raw image data from the simulator. It uses a pretrained ResNet-50 model to convert these images into high-level features, which are integral to the state representation in the MADDPG algorithm. This conversion process involves transforming the image into a suitable format, resizing it, and applying the ResNet-50 model. This capability allows the class to provide meaningful input for the reinforcement learning agent’s policy, making it particularly useful in visual tasks such as autonomous driving. 



* *

*Figure 6. MADDPG based on local experiences. *

20 





*Figure 7. MADDPG based on global shared experiences. *



*Figure 8. Components of agents in MADDPG *

To achieve our set objectives to answer our research questions described in Section 1.3, we have selected to teach the AV a specific learnable behavior - that AVs would cooperate \(based on global reward function\) at an uncontrolled intersection by making safe and comfortable decisions that follow the priority to the right rule. In a granular format, we have the following targets: 

1. that an AV approaching the intersection should detect other vehicles within the intersections. 

2. that the AV should detect whether there is a vehicle to its right and whether it’s moving toward the intersection. 

3. that the AV should slow down and eventually stop, indicating that it is giving way to the vehicle to its right. 

4. that the AV, although has given way, will continue in its current speed and direction if the AV to its right beyond a threshold distance of 50 m. 

5. the AV with the right of way should continue in its current speed or trajectory if the vehicle to its left is slowing down or stopping; otherwise, the AV should stop and give way to avoid a collision. 

During training in the simulation, we deployed 2 AVs controlled by the MADDPG close to an intersection, then used reward schemes to punish and compensate agents appropriately until they could perform the above-mentioned behaviors. Theoretically, as stated earlier, we formulate the problem as a multi-agent problem in a non-stationary environment. Each agent takes an action in the environment and contributes to the cumulative shared reward. We represent the state space as a vector or a multidimensional array that captures the values of several variables described below for each AV. Each AV updates its state representation at each time step as the AVs perceive the environment, take actions, receive feedback or new information, and contribute learned behavior to relay buffer \(stores experiences\). The state space is used as input to the Cooperative MADDPG algorithm for cooperative decision-making among AVs at the intersection. These are the variables we derive to represent the multi-dimensional state space for policy learning: 

1. Position: The position of each AV at the intersection, which we represent as coordinates \( *x*, *y*\) on a 2D plane or a grid-based representation. 

21 

2. Velocity: The velocity of each AV, which we represent as a vector \( *vx*, *vy*\) indicating the speed and direction of the vehicle. 

3. Heading: The heading or orientation of each AV, which we represent as an angle θ indicating the direction the vehicle faces. 

4. Traffic: The presence of other AVs or traffic near the intersection, which we represent as a binary variable indicating the presence or absence of other vehicles in each lane or approaching the intersection from different directions. 

5. Right-of-way status: A binary variable indicating whether the AV \(each AV\) has the right-of-way at the intersection according to the *"The priority to the right" * rule. 1 indicates that the AV has the right-of-way, and 0 indicates that the AV does not have the right-of-way. 

6. Action history: The history of actions taken by each AV, including the previous actions and their outcomes, is represented as a sequence of continuous actions the vehicle takes. 

7. Observation space: We attach RGB cameras to the AVs when they spawn in the simulation; we collect surrounding information in the environment of the AV using the camera. The collected information includes other vehicles, road markings, traffic signs, NPC \(Non-Player Actors\), and obstacles. 





22 



**6**. **Design** **Validation** **and** **Demonstration** 

**6.1. Training Simulation Environment Setup and Description** 

To validate the design, we set up a simulation environment to train the MARL. The simulation environment consists of setting up the CARLA simulation tool, configuring the simulation, defining agents and policies, implementing shared Multi-agent Relay Buffer and Individual Relay Buffer, and training agents in the CARLA environment. We train the MARL with one scenario modeled after one type of uncontrolled intersection - the T-junction \(See Figure 9\) below. 

The environment consists of a T-Junction where one road ends at a junction with another road. The experiment was in two variants. The first was performed using the CoMADDPG based on a \(local\)individualized relay buffer where experiences are not shared. Second, the CoMADDPG with a shared relay buffer where all agents contribute their experiences for learning by other agents. We train the agents for 5000 episodes with 1000 steps per episode while tuning the hyperparameters to optimized learning. 

We deployed two autonomous vehicles controlled by the MADDPG algorithm. 





*Figure 9. Design validation: training scenario at a T-Junction *

These vehicles start at various spawning \(points on the roads in the simulation tool where vehicles can be placed\) locations in the environment. Car A \(yellow car\) is coming from the right and is expected to turn left. Car B \(red car\), on the other hand, will approach from the left, intending to go straight, Figure 9 above. 

The goal of each vehicle is to navigate through the T-Junction and reach a specified destination while adhering to traffic rules, avoiding col isions, and maintaining a smooth and efficient driving pattern by learning the policies defined in Section 5.5 above. The reward is designed to encourage the desired behaviors. In the T-Junction scenario, the reward function is designed to promote learning abilities for the AV. \(1\) Adherence to the priority of the right rule. \(2\) Collision Avoidance. Vehicles should avoid colliding with each other and with static objects in the environment. \(3\) Smooth Driving - Abrupt actions should be discouraged. 

The agents’ performance during training was based on the fol owing metrics to ensure passenger safety and comfort. The average cumulative reward over the entire 5000 episodes and the smoothness of driving monitor for sudden changes in direction or speed that could indicate poor driving behavior. During each episode, autonomous vehicles used the MADDPG algorithm to select actions based on their current states. 

The CarlaEnvironmentWrapper will translate these actions into commands for the CARLA simulator to control the AV in the simulator, extract the new state from the simulator, calculate the reward based on the vehicles’ actions and states, and check if the episode has ended. 

This T-Junction scenario can test whether the MADDPG algorithm can effectively coordinate the actions of multiple autonomous vehicles in a complex traffic situation. This includes whether the vehicles can successfully navigate the T-Junction, adhere to traffic rules, avoid collisions, and reach their destinations efficiently. 

23 





**7. Model Evaluation in Simulated Environment **

We set up a four-way crossing to evaluate our model’s robustness to handle HDVs or adversarial drivers, as shown in Figure 10. Four evaluation scenarios were used to precisely assess the performance of the MADDPG algorithm and the CarlaEnvironmentWrapper. \(1\) Global experience relay buffer based MADDPG 

in the presence of an adversarial driver in the environment. \(2\) Global experience relay buffer based MADDPG in the absence of an adversarial driver in the environment. \(3\) Local experience relay buffer based MADDPG in the presence of an adversarial driver in the environment, \(4\) Local experience relay buffer based MADDPG in the absence of an adversarial driver in the environment. The goal is to assess how well our trained MADDPG agents have learned to act at an uncontrolled intersection. 





*Figure 10. Evaluation Scenario *

We consider a complex urban environment, such as a four-way intersection, for evaluation to test our model’s robustness. Under scenario 1, we deploy two autonomous vehicles controlled by the MADDPG 

based global experience relay buffer algorithm in the environment. These vehicles have already been trained, and their performance is being evaluated. In scenario 2, we repeat scenario one, but we spawn a third AV set to mimic HDV with random behavior, including sometimes not adhering to traffic rules. This unpredictable element added real-world complexity, mirroring situations that AVs would likely encounter in everyday traffic. Under scenario 3, we deploy two autonomous vehicles controlled by the MADDPG 

based local experience relay buffer algorithm in the environment. In scenario 4, we repeat scenario three and the third HDV/Adversarial driver. 

The goal of each vehicle is to navigate through the uncontrolled intersection and reach a specified destination while following traffic rules \(obeying the priority to the right rule\), avoiding collisions, and maintaining efficient and smooth driving. This evaluation was repeated over 1,000 episodes to gather a broad range of data and to allow the model’s behavior patterns to emerge. This helped us observe how the model’s policy evolved and adapted over time to navigate the intersection safely and efficiently, providing us with valuable insights into the learned behavior of the model. 

The crux of our research revolves around answering critical questions regarding the decision-making process of autonomous vehicles \(AVs\) at uncontrolled intersections. The primary objective was to examine the safety and comfort levels of the decisions made by AVs. To thoroughly investigate this, we designed a data collection strategy that revolved around four evaluation scenarios described above, each crafted to challenge our reinforcement learning model, a Multi-Agent Deep Deterministic Policy Gradient \(MADDPG\) agent. 

One critical data we collected was the collision rate, which provided a direct safety measure. Defined as the frequency of collisions between AVs at the intersection, this metric served as a critical indicator of the effectiveness of our MADDPG agent in avoiding accidents. We also evaluated how introducing the adversarial driver impacted this collision rate, testing our model’s robustness and adaptability to unexpected events. 

24 

To assess the comfort levels provided by our MADDPG agent’s control, we collected data on the Passenger Comfort Index \(PCI\). This comprehensive metric considers several factors, such as jerk \(rate of change of acceleration\), ride smoothness, and lane deviation. Higher PCI values correspond to better passenger comfort, offering a nuanced understanding of the quality of the driving experience beyond just safety considerations. 

These evaluation scenarios will give an insight into how well the MADDPG algorithm powered AVs cooperate to avoid collisions at the intersection while not sacrificing comfort. It will also allow us to assess the performance of global and local experience-based models. 





25 

**8. Results **

The results from these metrics, which were derived from collected and analyzed data, formed the basis of our findings. This allowed us to delve deep into understanding how a reinforcement learning model, like MADDPG, can effectively control AVs, ensuring safety and a comfortable riding experience, even in challenging and unpredictable traffic scenarios. We present the results of the metrics collected from training and evaluation in this section. 



*Table 1: Comparing training rewards for shared and individual learning experience. *





Global experience 

Global experience 

Relay Buffer 

Every 1000th episode Relay Buffer MADDPG MADDPG 

1. 1 - 1000 

1. 95% 

1. 96.1% 



2. 1001 - 2000 

2. 63% 

2. 79% 

Percentage 

3. 2001 - 3000 

3. 31% 

3. 45% 

Collision 

for Every 

4. 3001 - 4000 

4. 15% 

4. 33% 

1000th 

Episode 

5. 4001 - 5000 

5. 3% 

5. 20% 

1. 1 - 1000 

1. 5% 

1. 1% 



2. 1001 - 2000 

2. 21.7% 

2. 25.9% 

Percentage 

3. 2001 - 3000 

3. 55% 

3. 38% 

Successful 

Yield for 

4. 3001 - 4000 

4. 81% 

4. 51% 

Every 1000 

Episode 

5. 4001 - 5000 

5. 99.11% 

5. 79% 

1. 1 - 1000 

1. 95% 

1. 99% 



2. 1001 - 2000 

2. 78.3% 

2. 74.1% 

Percentage 

3. 2001 - 3000 

3. 45% 

3. 62% 

Unsuccessful 

yield for Every 

4. 3001 - 4000 

4. 19% 

4. 49% 

1000 

Episode 

5. 4001 - 5000 

5. 0.89% 

5. 21% 



To understand our first research question and fourth research objective, we collected information on average reward accumulation, average PCI to measure comfort, and collision rate to measure safety during evaluation. Figure 11 compares average reward accumulation progress through 5000 episodes between global experience relay buffer MADDPG and local experience relay buffer MADDPG. Figure 12 compares the average PCI between the global experience relay buffer and the local experience relay buffer. The table above represents collision rates, yield rates, and failed yield rates. 

26 





*Figure 11. Average reward accumulation comparison of Global and Local Experience Relay Buffer MADDPG *

*Models. *



*Figure 12. Average reward accumulation comparison of Global and Local Experience Relay Buffer MADDPG *

*Models *

For our research question two and the fifth objective, we collected data on mission completion rates for all four scenarios discussed in section 3. This was to give us an insight into how well our agents have learned and draw comparisons between the two models. The data is shown in Figures 13 and 14. We also collected data on PCI in all four scenarios shown in the frequency diagrams in Figures 15, 16, 17, and 18. This also will provide insight on how well the models are making safe decisions without compromising comfort. 

27 





*Figure 13. Successful/unsuccessful \(due to col ision\) rates with presence of an HDV \(adversarial driver\)* *Figure 14. Successful/unsuccessful \(due to col ision\) rates with absence of an HDV \(adversarial driver\)* 28 





\(a\) Frequency distribution of PCI for Global \(b\) Frequency distribution of PCI for Experience trained agents Local Experience trained agents 



*Figure 15. PCI Frequency Distribution: Frequency Distribution During Training with Presence of Adversarial* *Driver *





\(a\) Frequency distribution of PCI for Global \(b\) Frequency distribution of PCI for Experience trained agents 

Local Experience trained agents 

*Figure 16. PCI Frequency Distribution: Frequency Distribution During Evaluation without an Adversarial* *Driver *





*Figure 17. PCI Comparison for Local experienced pool trained agents versus global experienced pool trained* *agents in the presence of an Adversarial driver. *

29 





*Figure 18. PCI Comparison for Local experienced pool trained agents versus global experienced pool trained* *agents in the absence of an Adversarial driver. *





30 

**9. Analysis and Discussion **

In this section, we analyze the results collected from training and evaluation of the CoMADDPG. 

Regarding training data, we analyzed the accumulated rewards, PCI, collision rates, yield rates, and failed yields data to understand how the MADDPG model maximizes these metrics during training. It is essential to comprehend that the driving principle of reinforcement learning \(RL\) models, such as MADDPG, is the maximization of earned rewards. This forms the basis of their learning process and, ultimately, their performance. 

Figures 11 and 12 provide an insightful perspective on reward and PCI maximization. The model started with a negative reward accumulation, marked at -40 for the global experience relay buffer model, whereas it was -30 for the local experience-based model. This is a typical characteristic of RL, in the early stages of RL training, reflecting the model’s primary focus on exploring its environment, commonly referred to as the exploration phase. During this period, the model typically takes random actions, often leading to suboptimal outcomes or even collisions in the case of AVs, resulting in negative rewards. This also reflects both models’ high collision and failed yield rates in the first 1000 episodes, as shown in Table 1 above. 

Similarly, PCI values are low in both models, starting at points below 0.1. 

However, as the training progressed, a clear upward trend was noticed in all the metrics. It marked a shift from the exploration to the exploitation phase, where the model started capitalizing on its learned policies. 

Eventually, the reward accumulation rose to a peak of 30 for the global experienced-based model and 10 

for the local experience-based model, illustrating the model’s effectiveness in learning to take more beneficial actions over time. Again, the same trend can be seen in the collision and failed yield rates as they dropped progressively to \(3% - global experience, 20% - local experience\) and \(0.89% - global experience, 21% - local experience\) respectively, while yield rates increase over the period to \(99.11% - global experience, 79% - local experience\). The trend was similar in both models, except that the global experience base model recorded high values in metrics, as seen in Figures 11 and 12 and Table 1. 

By analyzing collision rates and the PCI in shared and local experience training regimes, we aimed to evaluate whether sharing experiences during training can improve the safety and comfort of AV driving. 

The findings from this analysis could provide valuable insights to guide the design of future AV training regimes, making them safer and more comfortable for passengers. 

PCI follows a similar trend such that during the exploration phase, there are low figures, but as the training progresses, it gets better, peaking at 0.70 for the global experiences pool. The trend is the same for local experience variant training as well. 

Regarding the local experience pool, the reward accumulation trajectory was different. The learning process took a somewhat extended period to climb into the positive reward range, indicating that the learning efficiency was lower than that of the global experience variant. Yet, with more training iterations, the reward accumulation did improve, albeit slower, eventually culminating in a peak reward accumulation of 12. 

The comparative analysis of the reward accumulation under shared and local experiences highlights the advantage of the former. It accelerates the learning process and achieves a higher peak reward, underlining its superiority in training MADDPG for optimal performance. 

**9.1. Evaluating the Models’ Safety and Comfort Decision-making Ability in a** **Four-way Uncontrolled Intersection with an HDV \(adversarial driver\)** 

Within the safety paradigm, we examined how global experiences influence collision rates and the AV’s capacity to avoid dangerous situations. We posited that global experience training would allow AVs to understand better different traffic scenarios, especially those involving non-compliant drivers such as the adversarial driver in our second evaluation scenario. This understanding could enhance the AVs’ 

predictive abilities, potentially enabling them to anticipate and avoid collisions more effectively than their single-experience counterparts. 

31 

To thoroughly comprehend the first research question within the realm of safety, we deduced that our MADDPG model, trained on a foundation of global experience relay buffer, indeed fostered a safer driving environment than its counterpart trained on local experience relay buffer. This finding was vividly illustrated in Figures 13 and 14, demonstrating superior performance from AVs trained via a global experience relay buffer. 

In Figure 13, where we introduced an adversarial driver to the intersection, we noticed an interesting phenomenon: the presence of the adversarial driver led to a decrease in the mission completion rate. 

However, the shared-experience-trained AVs still outperformed those trained on local experiences. 

Specifically, when faced with the adversarial driver, the shared-experience-trained AVs completed 73% of all missions, compared to only 51% completion by the AVs trained on local experiences \(See Figure 13\). 

Without an adversarial driver \(See Figure 13\), the mission completion rate rose dramatically, demonstrating the adversarial driver’s impact on the AVs’ overall performance. Yet again, the AVs trained on global experiences led the pack, reaching a commendable completion rate of 96%, as opposed to the 77% recorded by the AVs trained on local experience. 

On the comfort front, we evaluated how global experiences impact the Passenger Comfort Index \(PCI\). A higher PCI, indicative of a more comfortable ride, is highly desirable in AVs. As vehicles share experiences and learn from one another, they will likely develop better driving strategies, ensuring smoother acceleration and deceleration, maintaining lane discipline, and making safe, comfortable turns. 

Global experiences could be pivotal in enhancing the understanding of speed variation and steering variation, both integral to the PCI. For instance, global experiences might enable one vehicle to learn from the abrupt speed changes or sharp turns made by another vehicle, thereby guiding the former to maintain a more consistent speed or execute smoother turns in similar situations. 

Shifting our focus to the comfortability of driving for AVs, a visual analysis of Figures 15a, 15b, and 17 

revealed a marked decrease in the PCI when an adversarial driver was introduced into the scenario. 

However, the decrease was more pronounced for AVs trained on local experience relay buffer, a finding vividly portrayed in Figures 16a, 16b and 18. This trend further emphasizes the importance of global experiences in the training of AVs, enhancing both safety and passenger comfort. 

We provide statistical analysis to assess the validity and integrity of the data collected. 

The analysis was carried out for three categories of the data we collected. The Average PIC for learning, Average PIC for individualized learning, and Average reward for shared and individualized learning. 

**9.2. Comparing Training Rewards for Shared and Individual Learning **

**Experience Algorithm** 

* *

*Table 2: Comparing training rewards for shared and individual learning experiences. *



Global experience learning 

Local experience learning 



Reward Variance 473.66581035643145 

290.7664496345708 



Mean Reward 

-2.1065580058141715 

-7.666453382995337 



Median Reward 

3.485567454171153 

-1.0829598160147134 





Confidence 

\(-2.7098104745625298, 

\(-8.139098565497102, 

interval 

-1.5033055370658133\) 

7.193808200493572\) 

1. U statistic 

1. 15038788.0 



Mann-Whitney U 

2. P-value 

2. 3.0252578167921517e-

Test 

69 

32 



Turning our attention to the average reward for dataset as shown in the Table 2, we see a substantial variance of around 473.67 for the global experience learning. This expansive spread of data points around the mean indicates a broad spectrum of reward values within global experience learning, pointing towards a dynamic and varied range of outcomes in this context. The average reward for local experiences’ dataset exhibits a minor variance of roughly 290.77, pointing towards a narrower spread of reward values for local experiences. 

When we compare the mean reward values, we find that global experiences yield a higher average reward than local experiences. Applying the Mann-Whitney U test to verify this trend further, we obtain a U 

statistic of 15038788.0 and a P-value that essentially equals zero. This rejects the null hypothesis and confirms a statistically significant difference between shared and local experiences regarding average rewards. 



**9.3. Evaluation of Shared Policy Trained Agent using Two Scenarios** 

On exploring the dataset for the presence of adversarial driver in the scene, we notice that the variance is approximately 0.0073 as shown in Table 3. This low variance suggests a relatively small dispersion of scores around the mean. Here, our data indicates consistency, revealing a set of results closely packed around the average, thus potentially hinting at a stable system or process underlying this aspect of our dataset. 

Conversely, our investigation into the absence of adversarial driver in the scene dataset demonstrates a further reduction in variance, down to about 0.0008. This lower variance points to an even tighter grouping of scores around the mean, implying a more consistent set of results than when an adversarial driver is present. The difference in variance between these two sets could signify the relative influence an adversarial driver has on the model’s performance or stability. 



*Table 3: Evaluation of policy-trained agent using two scenarios. *



Presence of adversarial Driver 

Absence of adversarial Driver 

Variance 

0.0008034963540322729 

0.007279515049507866 

Mean PCI 

0.850492689426319 

0.6503087640189015 

Median PCI 

0.8500689786713302 

0.6500679549628237 

Confidence 

interval 

\(0.8487358177302088, 

\(0.6450206682087533, 

0.8522495611224291\) 

0.6555968598290497\) 

1. U statistic 

1. 0.0 

2. P-value 

2. 0.0 

Mann-Whitney U 

Test 



The Mann-Whitney U test offers significant insights into our quest for a more nuanced understanding. This non-parametric statistical test results in a U statistic of 0.0 and a P-value of 0.0. This observation rejects the null hypothesis, providing strong evidence that the presence or absence of an adversarial driver significantly impacts performance. 



33 

**9.4. In-depth Analysis of Average PCI Metrics in Local Experiences** Upon examining the average PCI with adversarial driver in the scene data, we notice a variance of around 0.0131 as shown in Table 4. This degree of variability suggests a moderate spread of scores around the mean, hinting at some variability in PCI when an adversarial driver is involved. 

In contrast, our analysis of the average PCI without an adversarial driver in the scene data reveals a decreased variance of approximately 0.0075. This lower variance suggests less dispersion and implies a more uniform set of scores. The comparison of variances between the two data sets provides an initial indication of an adversarial driver’s potential impact on the PCI. 

This is further supported by the mean values, which show a considerably higher mean PCI for average PCI without an adversarial driver in the scene compared to average PCI with an adversarial driver in the scene. 

To statistically substantiate this difference, we turn again to the Mann-Whitney U test. The resulting U 

statistic of 38767.0 and a P-value that practically equals zero provide strong evidence of a statistically significant difference in average PCI in the presence and absence of an adversarial driver. 

Our comprehensive statistical analysis offers several key insights: an adversarial driver tends to correspond with less favorable performance metrics and lower average PCI. In contrast, global experiences are generally associated with higher rewards than individual ones. As we draw these conclusions, we must remember that these statistical observations were interpreted and applied within our research’s specific context and considerations. These results shed light on broad trends and patterns. To further understand our findings, we analyze the results in response to our research questions and objectives. 



*Table 4: Evaluation of local experiences learning policy trained agents with and without adversarial driver. *



Presence of adversarial Driver 

Absence of adversarial Driver 

Variance 

0.007547312087306573 

0.013120168455025534 

Mean PCI 

0.549574717959101 

0.2964104762580265 

Median PCI 

0.5543510321148284 

0.2912058667112164 

\(0.5441902320421061, 

\(0.28931113918752827, 

Confidence interval 0.5549592038760958\) 

0.3035098133285248\) 

1. U statistic 

. 38767.0 

. 

2. P-value 

2.078609917568941e-279 

Mann-Whitney U 

Test 





**9.4. Discussion **

Our findings, which delve into the safety and comfort decision-making capabilities of AVs trained using the MADDPG, resonate with prevailing literature. The agents effectively learned the desired behavior, adhering to the “priority to the right” rule, guided by a reward function elaborated under section 5. Our study is a pioneering endeavor that leverages MARL specifically for navigating uncontrolled intersections and adds a global relay buffer to the existing MADDPG model. By integrating global experiences during the training phase, we observed a marked enhancement in both passenger comfort and the safety decision-making process of AVs at intersections by about 20% and 40%, respectively. This is likely attributable to the AVs being trained on a comprehensive and varied set of experiences from multiple agents. 

34 

The supremacy of global experiences over local experiences in training MADDPG aligns with the conclusions drawn by \[20\], who examined the impact of collective learning in multi-agent scenarios. They discovered that agents trained on global experiences tend to make more cooperative decisions, leading to better overall system performance, akin to our increased mission completion rates with training. 

The role of adversarial drivers in our scenarios and their impact on safety and comfort is like the work of 

\[97\], who incorporated adversarial vehicles to challenge their RL algorithms. The challenges presented by these adversarial drivers forced the RL algorithms to learn robust policies, mirroring our findings where the presence of the adversarial driver dropped the mission completion rates for both global and local experience base models, albeit lower in impact on the global experience relay buffer model AVs. 

Concerning passenger comfort, our emphasis on maintaining a high PCI reflects the research of \[85\]. They proposed a reward function considering comfort metrics, like a jerk and lane deviation, in training RL 

agents for self-driving cars. Their results indicated that agents trained with these rewards exhibited smoother driving characteristics, resonating with our observation of higher PCI values for global experience relay buffer trained AVs, even in the presence of an adversarial driver. 

As presented, the analysis of reward accumulation during training holds similarities with the research conducted by \[22\]. The authors, who first introduced the MADDPG model observed a similar pattern of initial negative rewards shifting to positive rewards as training progressed. They attributed this to the shift from the exploration phase to the exploitation phase, reinforcing our research findings. 

The contrast in reward accumulation patterns between global and local experiences can be compared to the work by \[31\]. They concluded that sharing experiences in multi-agent settings led to faster convergence during learning, resulting in a higher cumulative reward. This observation aligns seamlessly with our analysis, highlighting the accelerated learning process and improved peak rewards for global experiences compared to local experiences. 

Research by \[98\] further supports our findings, where they demonstrated that sharing experiences between agents during training resulted in better performance. They observed that this was primarily due to agents learning from each other’s experiences, fostering an environment for collective learning. This mirrored the benefits of global experiences observed in our study. 

In the broader context of reinforcement learning \(RL\) training, \[99\] have emphasized the importance of balancing exploration and exploitation to maximize the accumulated reward. This balance, reflected in our analysis of reward accumulation, offers further insight into the practical training of MADDPG agents, underscoring the value of the global experience relay buffer over the local experience relay buffer. 

Our research’s analysis and findings resonate strongly with existing literature and further consolidate the pivotal role of global experiences in the effective training of MADDPG agents for autonomous driving. The findings profoundly impact the real-world training of AVs. 

By adopting MARL in real-world training scenarios, AVs may better understand how to navigate complex environments like uncontrolled intersections. This could significantly reduce the potential for accidents in such challenging areas. 

Incorporating global experiences from multiple agents can expedite the learning curve for individual AVs. 

Instead of each AV solely relying on its own experiences, it benefits from a collective pool of experiences, thus leading to faster and more robust learning. 

The study revealed that the focus on passenger comfort means that AVs trained using this method are concerned with reaching a destination and ensuring the journey is smooth and comfortable. This could lead to wider acceptance and trust in AVs by the public. 

Demonstrating that AVs can be trained to make safer decisions at intersections, especially in uncontrolled environments, could influence future regulations, insurance policies, and public perception regarding the ethical deployment of AVs. 

The wider discourse on autonomous vehicles \(AVs\) must consider the diverse driving regulations across various nations and regional entities. This scenario presents a pertinent inquiry: can an AV trained under the driving norms of one nation reliably and securely navigate roads in another country with potentially disparate rules? To illustrate, is an AV, conditioned to drive on the left, adept at traversing roads in Sweden, where the right-hand drive is the norm? A potential solution could be amalgamating global experiences, wherein AVs trained under diverse regulations contribute their insights to a unified knowledge repository. 

Such a collective approach could significantly enhance the holistic training of AVs. 

35 

Global shared experiences will provide large training data sets for AVs. AVs will benefit from diverse road conditions, weather scenarios, driving behaviors, and infrastructural variations. This helps ensure that AVs are not just trained for specific regions but can adapt to global conditions. Sharing experiences and data means AVs don’t have to encounter every possible situation to learn from it individually. They can leverage the experiences of other vehicles in different regions, accelerating their learning process. Instead of each entity or country independently investing in generating diverse training data, shared data pools can distribute costs and provide access to high-quality data at reduced costs. 

Driving cultures vary across regions. Understanding and adapting to local driving nuances, pedestrian behavior, and regional gestures can be crucial for the smooth operation of AVs. A shared learning experience will integrate these cultural aspects into AV training. 

A global shared learning approach for AVs can bridge regional gaps, reduce redundancies, and provide a holistic, enriched dataset that ensures AVs are safer, more efficient, and universally adaptable. As discussed in this study, applying globally shared experience MARL can revolutionize how AVs are trained, making them safer, more efficient, and more aligned with real-world requirements and expectations. 





36 

**10. Limitations, Further Studies, and Conclusion **

**10.1. Limitations **

The primary limitation is the computational load that CARLA and MADDPG demand. Increasing the number of episodes from 5000 to 7000 or even 10,000 could have improved performance for the MADDPG models. 

The performance of RL algorithms primarily depends on the quantity and diversity of experiences they are exposed to during training. In the context of our work, more episodes translate to more driving experiences, which can cover a broader range of scenarios in the uncontrolled intersection. It can enable agents to learn more nuanced cooperative strategies that are not fully understood or experienced in the current 5000 episodes. 

While the CARLA simulator offers a high-definition and realistic environment for AV testing, there is an inherent limitation in how well it can mimic real-world driving conditions. The simulation’s accuracy concerning complex weather conditions, pedestrian behaviors, or sudden unexpected events might not fully capture the intricacies of actual driving scenarios. Despite using MADDPG to manage non-stationary environments, real-world environments are far more dynamic. Factors like human drivers’ behavior, dynamic traffic flow, and real-time changes in traffic rules or road conditions can pose challenges not addressed in the simulation. 

The above limitations could also guide future work to improve further the methodology and the effectiveness of AVs navigating uncontrolled intersections. 



**10.2. Conclusion **

Our research was driven by two research questions: 

1. How can multi-agent reinforcement learning improve autonomous vehicles’ safety and comfort decision-making capabilities in uncontrolled intersections, particularly in scenarios where Avs interact with HDVs \(Adversarial Drivers\)? 

2. To what extent can a multi-agent reinforcement learning approach with global experiences enhance passenger safety and comfort in AVs at uncontrolled intersections compared to local \(individual\) experiences MARL? 

In response to the first question, our research conclusively affirms that leveraging global experiences substantially enhances the optimization of MADDPG models, particularly in autonomous driving. A detailed examination of diverse scenarios revealed that MADDPG agents, when trained to utilize global experiences, not only fostered safer driving practices but also ensured an elevated level of passenger comfort. 

Our findings dovetail with the existing body of literature on multi-agent reinforcement learning, reinforcing assertions put forth by \[20\], \[97\], and \[85\]. These findings highlight the collective learning advantages of the global experience relay buffer, the challenges imposed by erratic drivers, and the criticality of considering passenger comfort when training RL agents. 

Addressing the second question, delving deeper into the accumulated rewards data offered valuable insights into how MADDPG models maximize rewards during training. We unearthed that integrating global experiences expedited the learning process, facilitated a swift model transition from the exploration to the exploitation phase, and culminated in a superior peak reward. These observations corroborate the findings of \[22\], \[31\], and \[98\] in their research, along with reinforcing the principles of reinforcement learning articulated by \[99\]. 

Incorporating global experiences in training MADDPG agents bolsters their capabilities to navigate complex real-world scenarios, as evidenced by improved mission completion rates, heightened passenger comfort, and efficient reward maximization in simulation. Therefore, embedding global experiences in training protocols is a pivotal strategy for advancing autonomous vehicles, significantly enhancing their safety, comfort, and overall performance. 

37 

Perhaps more critically, our findings bear profound implications for the decision-making processes of autonomous vehicles. The improved performance of the MADDPG agents in complex, unpredictable driving scenarios underscores their potential to react appropriately and safely to real-world obstacles and events. This capability is a critical precursor to achieving Level 5 autonomy, where vehicles are expected to manage all aspects of the driving task under all conditions. This implies a significant stride towards autonomous vehicles’ ability to independently navigate intricate traffic environments, including uncontrol ed intersections, with heightened safety and efficiency. 

Given these findings, our research contributes to the ongoing discourse on enhancing autonomous vehicle technology through multi-agent reinforcement learning. We anticipate that these insights will underpin further research in this area and inform the development of sophisticated training methodologies for autonomous driving, thereby accelerating the journey toward full autonomy in autonomous vehicles. 

Our study bridges a crucial gap in the literature by delving into the potential of MARL, particularly the MADDPG model trained with global experiences, to enhance AVs’ decision-making capabilities in uncontrolled intersections. The enhanced safety metrics, even in the face of adversarial challenges, coupled with significant improvements in passenger comfort, strongly address the research questions posed at the outset. The broader implications of our findings, such as the potential influence on regulations and public perception, position MARL as a transformative approach in the real-world training of AVs. 

**10.3. Future studies **

Our research provides a significant foundation from which multiple avenues of further study can be developed. While our current research focuses on the uncontrolled intersection scenario, further investigations can be conducted in more diverse traffic environments. Another exciting field of study could be the incorporation of inter-agent communication. A shared communication protocol or language could further enhance the ability of the agents to collaborate and negotiate traffic scenarios. The implementation and effects of such communication mechanisms on the efficiency and safety of AVs would provide compelling insights. Additionally, further research should be conducted to identify the point of diminishing returns, where additional episodes contribute minimal improvement, as this can vary across different environments and tasks. Finally, another aspect worth investigating is the scalability of the multi-agent systems. As the number of agents increases, how does the system performance scale? This will be especially crucial in dense urban environments where numerous autonomous vehicles might need to interact simultaneously. 

By exploring these areas, we can continue to advance the understanding of MADDPG in the context of autonomous driving, paving the way for safer, more efficient autonomous vehicles. 





38 

**BIBLIOGRAPHY **

\[1\] B. Chen, D. Sun, J. Zhou, W. Wong, and Z. Ding, “A future intelligent traffic system with mixed autonomous vehicles and human-driven vehicles,” *Information Sciences*, vol. 529, pp. 59–72, 2020. 

doi: 

https://doi.org/10.1016/j. 

ins.2020.02.009. 

\[Online\]. Available: 

https://www.sciencedirect.com/ science/article/pii/S0020025520300736. 

\[2\] S.-J. Babak, S. A. Hussain, B. Karakas, and S. Cetin, “Control of autonomous ground vehicles: A brief technical review,” *IOP Conference Series: Materials Science and *

*Engineering*, vol. 224, no. 1, p. 012029, Jul. 2017. doi: 10.1088/1757899X/224/1/012029. \[Online\]. 

Available: https://dx.doi.org/10.1088/ 1757-899X/224/1/012029. 

\[3\] J. Maddox, “Improving driving safety through automation,” *National Highway Tra* ffi *c Safety* *Administration*, 2012. 

\[4\] J. M. Anderson, K. Nidhi, K. D. Stanley, P. Sorensen, C. Samaras, and O. A. Oluwatola, *Autonomous* *vehicle technology: A guide for policymakers*. Rand Corporation, 2014. 

\[5\] S. A. Bagloee, M. Tavana, M. Asadi, and T. Oliver, “Autonomous vehicles: Challenges, opportunities, and future implications for transportation policies,” *Journal of modern transportation*, vol. 24, pp. 

284–303, 2016. 

\[6\] J. Manyika, M. Chui, J. Bughin, R. Dobbs, P. Bisson, and A. Marrs, *Disruptive technologies: Advances* *that will transform life, business, and the global economy*. McKinsey Global Institute San Francisco, CA, 2013, vol. 180. 

\[7\] S. Chen, Z. Jian, Y. Huang, Y. Chen, Z. Zhou, and N. Zheng, “Autonomous driving: Cognitive construction and situation understanding,” *Science China Information Sciences*, vol. 62, no. 8, 2019. 

\[8\] N. Li, Y. Yao, I. Kolmanovsky, E. Atkins, and A. R. Girard, “Game-theoretic modeling of multi-vehicle interactions at uncontrolled intersections,” *IEEE Transactions on Intel igent Transportation Systems*, vol. 23, no. 2, pp. 1428–1442, 2022. doi: 10.1109/TITS.2020.3026160. 

\[9\] R. Gutiérrez-Moreno, R. Barea, E. López-Guillén, J. Araluce, and L. M. Bergasa, “Reinforcement learning-based autonomous driving at intersections in carla simulator,” *Sensors*, vol. 22, no. 21, 2022. doi: 10.3390/s22218373. \[Online\]. Available: https://www.mdpi.com/1424-

8220/22/21/8373. 

\[10\] *European *

*Commission, mobility *

*i*& 

*transport *

*- *

*road *

* *

*safety*, 

https://roadsafety.transport.ec.europa.eu/statistics-and-analysis/statisticsandanalysis-

archive/powered-two-wheelers/studies-moped-andmotorcycleaccidents\_en, Accessed: 2010-09-30. 

\[11\] *National center for statistics and analysis \(ncsa\) motor vehicle tra* ffi *c crash data resource page*, 

https://crashstats.nhtsa.dot.gov. 

\[12\] L. Wei, Z. Li, J. Gong, C. Gong, and J. Li, “Autonomous driving strategies at intersections: Scenarios, state-of-the-art, and future outlooks,” in *2021 IEEE International Intel igent Transportation Systems* *Conference \(ITSC\)*, 2021, pp. 44– 51. doi: 10.1109/ITSC48978.2021.9564518. 

\[13\] M. Kamal, G. Srivastava, and M. Tariq, “Blockchain-based lightweight and secured v2v communication in the internet of vehicles,” *IEEE Transactions on Intel igent Transportation Systems*, vol. 22, no. 7, pp. 3997–4004, 2021. doi: 10.1109/TITS. 2020.3002462. 

\[14\] A. Nshimiyimana, D. Agrawal, and W. Arif, “Comprehensive survey of v2v communication for 4g mobile and wireless technology,” in *2016 International Conference on Wireless Communications,* *Signal Processing and Networking \(WiSPNET\)*, IEEE, 2016, pp. 1722–1726. 

\[15\] S. K. Sahu, A. Mokhade, and N. D. Bokde, “An overview of machine learning, deep learning, and reinforcement learning-based techniques in quantitative finance: 

Recent progress and challenges,” *Applied Sciences*, vol. 13, no. 3, 2023. doi: 10. 

3390/app13031956. 

\[Online\]. 

Available: 

https://www.mdpi.com/20763417/13/3/1956. 

39 

\[16\] S. Dai, L. Li, and Z. Li, “Modeling vehicle interactions via modified lstm models for trajectory prediction,” *IEEE Access*, vol. 7, pp. 38287–38296, 2019. doi: 10. 1109/ACCESS.2019.2907000. 

\[17\] C. Lu, H. Wang, C. Lv, J. Gong, J. Xi, and D. Cao, “Learning driver-specific behavior for overtaking: A combined learning framework,” *IEEE Transactions on Vehicular Technology*, vol. 67, no. 8, pp. 6788–

6802, 2018. doi: 10.1109/TVT. 2018.2820002. 

\[18\] Z. Li, C. Lu, C. Gong, J. Gong, J. Li, and L. Wei, “Driver behavior modelling at the urban intersection via canonical correlation analysis,” in *2020 3rd International Conference on Unmanned Systems \(ICUS\)*, 2020, pp. 564–569. doi: 10.1109/ ICUS50048.2020.9274914. 

\[19\] M. Volodymyr *et al. *, “Human-level control through deep reinforcement learning,” *Nature*, vol. 518, no. 8, 2015. 

\[20\] K. Zhang, Z. Yang, and T. Bas¸ar, *Multi-agent reinforcement learning: A selective overview of theories* *and algorithms*, 2019. doi: 10.48550/ARXIV.1911.10635. 

\[Online\]. Available: 

https://arxiv.org/abs/1911.10635. 

\[21\] A. Tampuu *et al. *, “Multiagent cooperation and competition with deep reinforcement learning,” *PLOS *

*ONE*, vol. 12, Nov. 2015. doi: 10.1371/journal.pone. 0172395. 

\[22\] R. Lowe, Y. I. Wu, A. Tamar, J. Harb, O. Pieter Abbeel, and I. Mordatch, “Multiagent actor-critic for mixed cooperative-competitive environments,” *Advances in neural information processing systems*, vol. 30, 2017. 

\[23\] \[Online\]. 

Available: 

https://www.deepmind.com/blog/deepreinforcementlearning. 

\[24\] \[Online\]. Available: https://www.unite.ai/what-is-deep-reinforcementlearning/. 

\[25\] \[Online\]. 

Available: 

https://en.wikipedia.org/wiki/Multi-agent\_ 

reinforcement\_learning. 

\[26\] K. Zhang, Z. Yang, and T. Bas¸ar, *Multi-agent reinforcement learning: A selective overview of theories* *and algorithms*, 2021. arXiv: 1911.10635\[cs.LG\]. 

\[27\] F. A. Oliehoek and C. Amato, “Dec-POMDPs as non-observable MDPs,” Intelligent Systems Lab, University of Amsterdam, Amsterdam, The Netherlands, IAS technical report IAS-UVA-14-01, Oct. 

2014. 

\[28\] E. A. Hansen, D. S. Bernstein, and S. Zilberstein, “Dynamic programming for partially observable stochastic games,” in *Proceedings of the Nineteenth National Conference on Artificial Intel igence*, San Jose, California, 2004, pp. 709–715. \[Online\]. Available: 

http://rbr.cs.umass.edu/shlomo/papers/HBZaaai04. html. 

\[29\] J. Foerster, I. A. Assael, N. De Freitas, and S. Whiteson, “Learning to communicate with deep multiagent reinforcement learning,” *Advances in neural information processing systems*, vol. 29, 2016. 

\[30\] O. De Lima, H. Shah, T.-S. Chu, and B. Fogelson, “Efficient ridesharing dispatch using multi-agent reinforcement learning,” *arXiv preprint arXiv:2006.10897*, 2020. 

\[31\] J. Foerster, G. Farquhar, T. Afouras, N. Nardelli, and S. Whiteson, “Counterfactual multi-agent policy gradients,” in *Proceedings of the AAAI conference on artificial intel igence*, vol. 32, 2018. 

\[32\] T. Wu, M. Jiang, and L. Zhang, “Cooperative multiagent deep deterministic policy gradient \(comaddpg\) for intelligent connected transportation with unsignalized intersection,” *Mathematical* *Problems in Engineering*, vol. 2020, 2020. 

\[33\] K. Bimbraw, “Autonomous cars: Past, present and future a review of the developments in the last century, the present scenario and the expected future of autonomous vehicle technology,” in *2015 *

*12th International Conference on Informatics in Control, Automation and Robotics \(ICINCO\)*, vol. 01, 2015, pp. 191– 198. 

\[34\] L. S. Davis, D. Dementhon, R. Gajulapalli, T. R. Kushner, J. LeMoigne, and P. Veatch, “Vision-based navigation: A status report,” in *Proceedings of Image Understanding Workshop*, 1987, pp. 153–169. 

40 

\[35\] C. Thorpe, M. Herbert, T. Kanade, and S. Shafer, “Toward autonomous driving: The cmu navlab. i. 

perception,” *IEEE expert*, vol. 6, no. 4, pp. 31–42, 1991. 

\[36\] J. Redmon and A. Farhadi, “Yolov3: An incremental improvement,” *arXiv preprint arXiv:1804.02767*, 2018. 

\[37\] D. Cem, *Reinforcement learning: Benefits and applications in 2023*, https:// 

research.aimultiple.com/reinforcement-learning/, 2023. 

\[38\] Y. Shan, B. Zheng, L. Chen, L. Chen, and D. Chen, “A reinforcement learningbased adaptive path tracking approach for autonomous driving,” *IEEE Transactions on Vehicular Technology*, vol. 69, no. 

10, pp. 10581–10595, 2020. doi: 10. 1109/TVT.2020.3014628. 

\[39\] T. Chu, J. Wang, L. Codecà, and Z. Li, “Multi-agent deep reinforcement learning for large-scale traffic signal control,” *IEEE Transactions on Intel igent Transportation Systems*, vol. 21, no. 3, pp. 1086–

1095, 2020. doi: 10.1109/TITS.2019. 2901791. 

\[40\] E. Yurtsever, J. Lambert, A. Carballo, and K. Takeda, “A survey of autonomous driving: Common practices and emerging technologies,” *IEEE Access*, vol. 8, pp. 58443– 58469, 2020. doi: 

10.1109/ACCESS.2020.2983149. 

\[41\] W. N. Caballero, D. Rios Insua, and D. Banks, “Decision support issues in automated driving systems,” 

*International Transactions in Operational Research*, vol. 30, no. 

3, pp. 1216–1244, 2023. 

\[42\] J. SAE, “3016-2018, taxonomy and definitions for terms related to driving automation systems for on-road motor vehicles,” *Society of Automobile Engineers, sae. org*, 2018. 

\[43\] D. Bhatt, D. Sodhi, A. Pal, V. Balasubramanian, and M. Krishna, “Have i reached the intersection: A deep learning-based approach for intersection detection from monocular cameras,” in *2017 *

*IEEE*/ *RSJ International Conference on Intelligent Robots and Systems \(IROS\)*, 2017, pp. 4495–4500. 

doi: 10.1109/IROS.2017. 8206317. 

\[44\] L. Chen *et al. *, “Deep neural network based vehicle and pedestrian detection for autonomous driving: A survey,” *IEEE Transactions on Intel igent Transportation Systems*, vol. 22, no. 6, pp. 3234–3246, 2021. doi: 10.1109/TITS.2020.2993926. 

\[45\] Z. Chen and X. Huang, “Pedestrian detection for autonomous vehicle using multispectral cameras,” 

*IEEE Transactions on Intelligent Vehicles*, vol. 4, no. 2, pp. 211– 219, 2019. doi: 

10.1109/TIV.2019.2904389. 

\[46\] S. Gautam and A. Kumar, “Image-based automatic traffic lights detection system for autonomous cars: A review,” *Multimedia Tools and Applications*, pp. 1–48, 2023. 

\[47\] M. Bouton, A. Cosgun, and M. J. Kochenderfer, “Belief state planning for autonomously navigating urban intersections,” in *2017 IEEE Intelligent Vehicles Symposium \(IV\)*, 2017, pp. 825–830. doi: 

10.1109/IVS.2017.7995818. 

\[48\] D. Isele, R. Rahimi, A. Cosgun, K. Subramanian, and K. Fujimura, “Navigating occluded intersections with autonomous vehicles using deep reinforcement learning,” in *2018 IEEE International* *Conference on Robotics and Automation \(ICRA\)*, 2018, pp. 2034–2039. doi: 

10.1109/ICRA.2018.8461233. 

\[49\] K. Driggs-Campbell, V. Govindarajan, and R. Bajcsy, “Integrating intuitive driver models in autonomous planning for interactive maneuvers,” *IEEE Transactions on Intel igent Transportation* *Systems*, vol. 18, no. 12, pp. 3461–3472, 2017. 

\[50\] S. Atakishiyev, M. Salameh, H. Yao, and R. Goebel, “Towards safe, explainable, and regulated autonomous driving,” *CoRR*, vol. abs/2111.10518, 2021. arXiv: 2111. 10518. \[Online\]. Available: 

https://arxiv.org/abs/2111.10518. 

\[51\] H. Winner, *at - Automatisierungstechnik*, vol. 66, no. 2, pp. 100–106, 2018. doi: 

doi:10.1515/auto-2017-0106. \[Online\]. Available: https://doi.org/10. 1515/auto2017-0106. 

41 

\[52\] K. Muhammad, A. Ullah, J. Lloret, J. D. Ser, and V. H. C. de Albuquerque, “Deep learning for safe autonomous driving: Current challenges and future directions,” *IEEE Transactions on Intelligent* *Transportation Systems*, vol. 22, no. 7, pp. 4316– 4336, 2021. doi: 10.1109/TITS.2020.3032227. 

\[53\] D. Isele, A. Nakhaei, and K. Fujimura, “Safe reinforcement learning on autonomous vehicles,” *CoRR*, vol. abs/1910.00399, 2019. arXiv: 1910.00399. 

\[Online\]. Available: 

http://arxiv.org/abs/1910.00399. 

\[54\] N. Ghafoorianfar and M. Roopaei, “Environmental perception in autonomous vehicles using edge level situational awareness,” in *2020 10th Annual Computing *

*and Communication Workshop and Conference \(CCWC\)*, 2020, pp. 0444–0448. doi: 

10.1109/CCWC47524.2020.9031155. 

\[55\] C. Tang, J. Chen, and M. Tomizuka, “Adaptive probabilistic vehicle trajectory prediction through physically feasible bayesian recurrent neural network,” in *2019 International Conference on Robotics* *and Automation \(ICRA\)*, 2019, pp. 3846– 3852. doi: 10.1109/ICRA.2019.8794130. 

\[56\] Y. Rasekhipour, A. Khajepour, S.-K. Chen, and B. Litkouhi, “A potential fieldbased model predictive path-planning controller for autonomous road vehicles,” *IEEE Transactions on Intelligent* *Transportation Systems*, vol. 18, no. 5, pp. 1255– 1267, 2017. doi: 10.1109/TITS.2016.2604240. 

\[57\] S. Raúl and D. Duarte, “Driving in roundabouts: Why a different theory of expert cognition in social driving is needed for self-driving cars,” *Journal of Expertise*, vol. 4\(1\), 2021. 

\[58\] K. B. Naveed, Z. Qiao, and J. M. Dolan, “Trajectory planning for autonomous vehicles using hierarchical reinforcement learning,” in *2021 IEEE International Intel igent Transportation Systems* *Conference \(ITSC\)*, 2021, pp. 601–606. doi: 10. 1109/ITSC48978.2021.9564634. 

\[59\] I. Panagiotopoulos and G. Dimitrakopoulos, “Intelligent, in-vehicle autonomous decision-making functionality for driving style reconfigurations,” *Electronics*, vol. 12, no. 6, 2023. doi: 

10.3390/electronics12061370. 

\[Online\]. Available: https: 

//www.mdpi.com/2079-

9292/12/6/1370. 

\[60\] P. Hang, Y. Zhang, and C. Lv, “Brain-inspired modelling and decision-making for human-like autonomous driving in mixed traffic environment,” *CoRR*, vol. 

abs/2201.03125, 

2022. arXiv: 2201.03125. \[Online\]. Available: https://arxiv.org/abs/ 2201.03125. 

\[61\] J. McDowell, “How driving age and norms vary throughout the world,” Tech. Rep., 2022. 

\[62\] R. S. Sutton and A. G. Barto, “Reinforcement learning: An introduction mit press,” *Cambridge, MA*, vol. 22447, 1998. 

\[63\] K. Arulkumaran, M. P. Deisenroth, M. Brundage, and A. A. Bharath, “Deep reinforcement learning: A brief survey,” *IEEE Signal Processing Magazine*, vol. 34, no. 6, pp. 26–38, 2017. 

\[64\] O. Vinyals *et al. *, “Grandmaster level in starcraft ii using multi-agent reinforcement learning,” *Nature*, pp. 1–5, 2019. 

\[65\] J. Ma and F. Wu, “Feudal multi-agent deep reinforcement learning for traffic signal control,” in *Proceedings of the 19th International Conference on Autonomous Agents and Multiagent Systems* *\(AAMAS\)*, 2020, pp. 816–824. 

\[66\] G. Bono, J. S. Dibangoye, O. Simonin, L. Matignon, and F. Pereyron, “Solving multiagent routing problems using deep attention mechanisms,” *IEEE Transactions on Intel igent Transportation* *Systems*, vol. 22, no. 12, pp. 7804–7813, 2021. doi: 

10.1109/TITS.2020.3009289. 

\[67\] C. Finn, P. Abbeel, and S. Levine, “Model-agnostic meta-learning for fast adaptation of deep networks,” in *International conference on machine learning*, PMLR, 2017, pp. 1126–1135. 

\[68\] L. Bus¸oniu, R. Babuška, and B. De Schutter, “Multi-agent reinforcement learning: An overview,” 

*Innovations in multi-agent systems and applications-1*, pp. 183– 221, 2010. 

42 

\[69\] R. Lowe, Y. WU, A. Tamar, J. Harb, O. Pieter Abbeel, and I. Mordatch, “Multiagent actor-critic for mixed cooperative-competitive environments,” in *Advances in Neural Information Processing Systems*, I. 

Guyon *et al. *, Eds., vol. 30, Curran Associates, Inc., 2017. \[Online\]. Available: 

https://proceedings.neurips.cc/ 

paper\_files/paper/2017/file/68a9750337a418a86fe06c1991a1d64cPaper.pdf. 

\[70\] P. Sunehag *et al. *, “Value-decomposition networks for cooperative multi-agent learning,” *arXiv* *preprint arXiv:1706.05296*, 2017. 

\[71\] X. Lu *et al. *, “Reinforcement learning-based physical cross-layer security and privacy in 6g,” *IEEE *

*Communications Surveys and Tutorials*, vol. 25, no. 1, pp. 425– 466, 2023. doi: 

10.1109/COMST.2022.3224279. 

\[72\] M. Kolat, B. Kovári, T. Bécsi, and S. Aradi, “Multi-agent reinforcement learning˝ for traffic signal control: A cooperative approach,” *Sustainability*, vol. 15, no. 4, 2023. doi: 10.3390/su15043479. 

\[Online\]. Available: https://www.mdpi. com/20711050/15/4/3479. 

\[73\] X. Wang, L. Ke, Z. Qiao, and X. Chai, “Large-scale traffic signal control using a novel multiagent reinforcement learning,” *IEEE Transactions on Cybernetics*, vol. 51, no. 1, pp. 174–187, 2021. doi: 

10.1109/TCYB.2020.3015811. 

\[74\] Z. Huang and F. Tanaka, “Mspm: A modularized and scalable multi-agent reinforcement learningbased system for financial portfolio management,” *Plos one*, vol. 17, no. 2, e0263689, 2022. 

\[75\] Á. Serra-Gómez, B. Brito, H. Zhu, J. J. Chung, and J. Alonso-Mora, “With whom to communicate: Learning efficient communication for multi-robot collision avoidance,” in *2020 IEEE*/ *RSJ *

*International Conference on Intelligent Robots and Systems \(IROS\)*, 2020, pp. 11770–11776. doi: 

10.1109/IROS45743.2020.9341762. 

\[76\] H. Wei, G. Zheng, H. Yao, and Z. Li, “Intellilight: A reinforcement learning approach for intelligent traffic light control,” in *Proceedings of the 24th ACM SIGKDD International Conference on Knowledge* *Discovery and Data Mining*, ser. KDD ’18, London, United Kingdom: Association for Computing Machinery, 2018, pp. 2496– 2505. doi: 10.1145/3219819.3220096. \[Online\]. Available: https://doi. 

org/10.1145/3219819.3220096. 

\[77\] C.-C. Yen, H. Gao, and M. Zhang, “Deep reinforcement learning based platooning control for travel delay and fuel optimization,” in *2022 IEEE 25th International Conference on Intel igent* *Transportation Systems \(ITSC\)*, IEEE, 2022, pp. 737– 742. 

\[78\] D. Krajzewicz, G. Hertkorn, C. Rössel, and P. Wagner, “Sumo \(simulation of urban mobility\) - an open-source traffic simulation,” 2002. 

\[79\] H. Alghodhaifi and S. Lakshmanan, “Autonomous vehicle evaluation: A comprehensive survey on modeling and simulation approaches,” *IEEE Access*, vol. 9, pp. 151531–151566, 2021. doi: 

10.1109/ACCESS.2021.3125620. 

\[80\] M. Ma, S. M. Preum, M. Y. Ahmed, W. Tärneberg, A. Hendawi, and J. A. Stankovic, “Data sets, modeling, and decision making in smart cities: A survey,” *ACM Trans. Cyber-Phys. Syst. *, vol. 4, no. 2, Nov. 2019. 

doi: 10.1145/3355283. \[Online\]. Available: https://doi.org/10.1145/3355283. 

\[81\] S. Shah, D. Dey, C. Lovett, and A. Kapoor, *Airsim: High-fidelity visual and physical simulation for* *autonomous vehicles*, 2017. arXiv: 1705.05065\[cs.RO\]. 

\[82\] B. Alvey, D. T. Anderson, A. Buck, M. Deardorff, G. Scott, and J. M. Keller, “Simulated photorealistic deep learning framework and workflows to accelerate computer vision and unmanned aerial vehicle research,” in *2021 IEEE*/ *CVF International Conference on Computer Vision Workshops \(ICCVW\)*, 2021, pp. 3882– 3891. doi: 10.1109/ICCVW54120.2021.00435. 

\[83\] V. Sadhu, C. Sun, A. Karimian, R. Tron, and D. Pompili, “Aerial-deepsearch: Distributed multi-agent deep reinforcement learning for search missions,” Dec. 2020, pp. 165–173. doi: 

10.1109/MASS50613.2020.00030. 

\[84\] K. Nagami and M. Schwager, “Hjb-rl: Initializing reinforcement learning with optimal control policies applied to autonomous drone racing.,” in *Robotics: science and systems*, 2021. 

43 

\[85\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, “Carla: An open urban driving simulator,” 

in *Conference on robot learning*, PMLR, 2017, pp. 1–16. 

\[86\] W. Wang, L. Wang, C. Zhang, C. Liu, and L. Sun, “Social interactions for autonomous driving: A review and perspectives,” *Foundations and Trends*® *in Robotics*, vol. 10, no. 3-4, pp. 198–376, 2022. doi: 

10.1561/2300000078. \[Online\]. Available: http://dx.doi.org/10.1561/2300000078. 

\[87\] G. Sistu, I. Leang, and S. Yogamani, *Real-time joint object detection and semantic segmentation* *network for automated driving*, 2019. arXiv: 1901.03912\[cs.CV\]. 

\[88\] A. Hevner, S. Chatterjee, A. Hevner, and S. Chatterjee, “Design science research in information systems,” *Design research in information systems: theory and practice*, pp. 9–22, 2010. 

\[89\] K. Peffers, T. Tuunanen, M. A. Rothenberger, and S. Chatterjee, “A design science research methodology for information systems research,” *Journal of management information systems*, vol. 

24, no. 3, pp. 45–77, 2007. 

\[90\] S. Gregor, D. Jones, *et al. *, “The anatomy of a design theory,” Association for Information Systems, 2007. 

\[91\] K. Peffers *et al. *, “Design science research process: A model for producing and presenting information systems research,” *ArXiv*, vol. abs/2006.02763, 2020. 

\[92\] V. K. Vaishnavi and W. Kuechler, *Design science research methods and patterns: innovating* *information and communication technology*. Crc Press, 2015. 

\[93\] J. v. Brocke, A. Hevner, and A. Maedche, “Introduction to design science research,” in Sep. 2020, pp. 

1–13. doi: 10.1007/978-3-030-46781-4\_1. 

\[94\] J. T. Wixted and S. L. Thompson-Schill, *Stevens’ Handbook of Experimental Psychology and Cognitive* *Neuroscience, Language and Thought*. John Wiley & Sons, 2018, vol. 3. 

\[95\] P. Johannesson and E. Perjons, “A method framework for design science research,” in *An Introduction* *to Design Science*. Cham: Springer International Publishing, 2021, pp. 77–93. doi: 10.1007/978-3-

030-78132-3\_4. \[Online\]. Available: https://doi.org/10.1007/978-3-030-78132-3\_4. 

\[96\] J. vom Brocke, A. Hevner, and A. Maedche, “Introduction to design science research,” in *Design* *Science Research. Cases*, J. vom Brocke, A. Hevner, and A. Maedche, Eds. Cham: Springer International Publishing, 2020, pp. 1–13. doi: 10. 1007/978-3-030-46781-4\_1. \[Online\]. Available: 

https://doi.org/10. 1007/978-3030-46781-4\_1. 

\[97\] E. Vinitsky *et al. *, “Benchmarks for reinforcement learning in mixed-autonomy traffic,” in *Conference* *on robot learning*, PMLR, 2018, pp. 399–409. 

\[98\] S. Iqbal and F. Sha, “Actor-attention-critic for multi-agent reinforcement learning,” in *International* *conference on machine learning*, PMLR, 2019, pp. 2961–2970. 

\[99\] R. S. Sutton and A. G. Barto, *Reinforcement learning: An introduction*. MIT press, 2018. 

44 

**APPENDIX **

**Implementation Details **

We implemented a CarlaEnvironmentWrapper class, which interfaces with the simulator, providing methods to initialize the simulation, extract states, execute actions, calculate rewards, and check for termination conditions. The class also transforms raw image data into a format suitable for a neural network using a pre-trained ResNet-50 model. 

Reset method: The reset method starts a new episode in the simulation, resetting the state of the environment and the vehicles. It returns to the initial state of the environment. 

Step method: The step method takes a list of actions \(one for each vehicle\) and applies them in the simulation. It then advances the simulation by a one-time step, calculates the reward for each vehicle, and checks if the episode has terminated \(e.g., if a vehicle has reached its destination or if a maximum number of steps has been reached\). It returns the new state, the rewards, and a list of boolean flags indicating whether each vehicle’s episode has terminated. 

State extraction: The function is used to process the raw image data from the simulator. It resizes the image, preprocesses it for the ResNet-50 model, and then uses the ResNet50 

model to extract features from the image. These features form part of the state representation used by the MADDPG algorithm. Here’s a breakdown of what each step in the feature extraction does: 

Preprocessing the image: The raw image data is converted into a format that can be input into the ResNet50 model. First, we convert the image array to a PIL \(Python Imaging Library\) Image instance. The image is resized to 224x224 pixels. This is the standard input size for the ResNet50 model. The PIL Image instance is converted to a NumPy array so the ResNet50 model can process it. A new dimension is added to the array, representing the batch size. This is done because deep learning models process images in batches. Even though there’s only one image here, it must still be in a batch format. Extracting features: The preprocessed image is passed through the ResNet50 model to extract high-level features. The output of the model is saved in the features variable. The output represents high-level features of the image that the model has learned to recognize. This method is important because it allows the CarlaEnvironmentWrapper class to extract meaningful features from raw images, which can be input into the agent’s policy. This is particularly useful in tasks involving visual input, such as autonomous driving, where an agent needs to understand high-level visual features, like the presence of other cars, pedestrians, or road markings, to make appropriate decisions. 

Termination check: The class has a method to check for termination conditions, such as a vehicle reaching its destination or if the maximum number of steps of 1000 per episode has been reached. 

**DDPG Agent Class Structure **

The DDPG agents consist of four main classes, Replay-Buffer: This class is a data structure used to store previous experiences or transitions that the agent can use for learning. These experiences are tuples of the state, action, reward, next state, and whether the episode ended in this state \(done\). The Replay-Buffer uses a deque \(double-ended queue\) from Python’s collections module for storing experiences because of its efficient append and pop 



operations. The sample function randomly selects a batch of experiences from the buffer for learning. 

Actor: This class represents the actor model in the actor-critic methodology. It is a simple neural network with three linear layers and uses a ReLU activation function for the first two layers. The final layer uses a *tanh * activation function, scaled by the maximum action value. 

The actor takes the state of the environment as input and outputs the bestbelieved action. 

Critic: This class represents the critic model in the actor-critic methodology. It is also a neural network, like the Actor model, but differs in the input and output layers. The Critic takes a state-action pair as input and outputs a Q-value, indicating the ’quality’ of that action in the given state. 

DDPG: This class encapsulates the entire deep-deterministic policy gradient algorithm. The class initializes an actor, a critic model, and a target model for each. Target models stabilize learning and are slowly updated to the main models over time, controlled by a factor *tau*. 

The select action method in this class uses the actor model to determine the best action to take in each state. The training method runs the main learning loop, which involves interacting with the environment, storing experiences in the replay buffer, sampling batches of experiences to learn from, and updating the actor and critic models based on these experiences. 

**Code structure and Implementation of the MADDPG Environment **

In this environment, there are three classes, MADDPG, OUNoise, and MultiAgentReplayBuffer. The MADDPG have two functionalities to train and evaluate. 

Train: This function trains the agents using the MADDPG algorithm. It takes the environment, agents, replay buffer, number of episodes, batch size, noise scale, and training interval as input arguments. The function starts by initializing exploration noise and running through each episode. During an episode, it selects actions for each agent, executes the actions in the environment, and adds the experiences to the replay buffer. Once the replay buffer contains enough experience for all agents, the agents are trained centrally. 

Each agent learns from their experiences or global experiences and updates their actor and critic models. The function also calculates and logs the average critic and actor loss values during training. 

Evaluate: This function is responsible for evaluating the performance of the trained agents. 

It takes the environment, agents, and the number of evaluation episodes as input arguments. 

The function runs through each evaluation episode and selects actions for each agent without exploration noise. It executes the actions in the environment and accumulates rewards during the episode. The function returns the total rewards obtained during the evaluation. 

We also implemented OUNoise class, which implements the Ornstein-Uhlenbeck process, a stochastic process often used in reinforcement learning to add exploration noise to the agent’s action selection. This noise process is characterized by the correlation of noise in time, which can be beneficial in physical control problems, where the next action is often correlated with the previous one. 

The key components of the OUNoise class are the reset method which resets the state of the noise process to the long-term mean *mu*. This method is typically called at the beginning of each episode. The sampling method updates the state of the noise process and returns it as a noise sample. The update equation represents the OrnsteinUhlenbeck process, which generates temporally correlated noise. 



In the context of the MADDPG algorithm, the OUNoise class is used to add exploration noise to the actions selected by the policy \(or actor\) network. This encourages the agent to explore the environment and helps to prevent the agent from getting stuck in local optima. The noise is added to the action in the training method. 

By adding correlated noise over time, the agents are encouraged to maintain a direction of exploration for several time steps, rather than changing direction randomly at each time step. This was beneficial in control tasks, where the actions control velocities or acceleration, so smooth activity changes can lead to more effective state space exploration. 

We implemented a “MultiAgentReplayBuffer” class which manages the storage and sampling of experiences for multiple agents in a multi-agent reinforcement learning scenario. Each agent has its replay buffer \(implemented as a Python deque with a specified maximum length\) where its experiences \(state, action, reward, next state, done\) are stored. 

This implementation was updated to a shared relay buffer in other experiments. Key components of the “MultiAgentReplayBuffer” class are the add method used to add an experience to the buffer of a specific agent. The experience consists of the state, action, reward, next state, and done flag. The done flag indicates whether the episode has ended. 

The sampling method samples a batch of experiences from each agent’s or shared buffer. It first checks whether the buffer has enough experience for a batch. If so, it samples a batch of experiences from each buffer and stacks them into Numpy arrays. The method returns a list of batch data, one for each agent. If any agent’s buffer lacks experience, the method returns None. This class is crucial for the MADDPG algorithm because it independently handles each agent’s storage and retrieval of experiences. This allows for efficient training of each agent using its own/s, a key aspect of multi-agent reinforcement learning. 




# Document Outline

+ Popular science summary 
+ Abstract 
+ LIST OF FIGURES 
+ LIST OF TABLES 
+ 1. Introduction  
	+ 1.1. Background 
	+ 1.2. Research Goals and Motivation 
	+ 1.3. Research Questions 
	+ 1.4. Purpose, and Objectives 

+ 2. Theoretical Background  
	+ 2.1. Deep Reinforcement Learning Algorithms 
	+ 2.2. Multi-agent Frameworks 
	+ 2.3. Cooperative MARL 
	+ 2.4. Algorithms in Cooperative MARL 

+ 3. Literature Review  
	+ 3.1. History of Autonomous Vehicle 
	+ 3.2. Emerging Technologies in AV industry.  
	+ 3.3. Intersection and Autonomous Vehicles 
	+ 3.4. Safety and Comfort Decision-Making in Autonomous Vehicles 
	+ 3.5. Reinforcement Learning 
	+ 3.6. Multi Agent Reinforcement Learning \(MARL\) 
	+ 3.7. Overview of Simulators 

+ 4. Research Methodology  
	+ 4.1. Design Science 
	+ 4.2. Application of design science in this research 

+ 5. Design and Implementation  
	+ 5.1. Deep Deterministic Policy Gradient Algorithm 
	+ 5.2. Multi-agent Deep Deterministic Policy Gradient 
	+ 5.2. Cooperative MADDPG Policy for Global Shared Experience Buffer 
	+ 5.3. Learning Policy 
	+ 5.4. Rewards Definition 
	+ 5.5. The Simulated Environment 

+ 6. Design Validation and Demonstration 
+ 6.1. Training Simulation Environment Setup and Description 
+ 7. Model Evaluation in Simulated Environment 
+ 8. Results 
+ 9. Analysis and Discussion  
	+ 9.1. Evaluating the Models’ Safety and Comfort Decision-making Ability in a Four-way Uncontrolled Intersection with an HDV \(adversarial driver\) 
	+ 9.2. Comparing Training Rewards for Shared and Individual Learning 
	+ Experience Algorithm 
	+ 9.3. Evaluation of Shared Policy Trained Agent using Two Scenarios 
	+ 9.4. In-depth Analysis of Average PCI Metrics in Local Experiences 
	+ 9.4. Discussion 

+ 10. Limitations, Further Studies, and Conclusion  
	+ 10.1. Limitations 
	+ 10.2. Conclusion 
	+ 10.3. Future studies 

+ BIBLIOGRAPHY 
+ APPENDIX  
	+ Implementation Details 
	+ DDPG Agent Class Structure 
	+ Code structure and Implementation of the MADDPG Environment



