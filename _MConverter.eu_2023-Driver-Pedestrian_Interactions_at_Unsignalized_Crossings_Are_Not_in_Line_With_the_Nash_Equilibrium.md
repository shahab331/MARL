Received 8 September 2023, accepted 4 October 2023, date of publication 9 October 2023, date of current version 12 October 2023. 

*Digital Object Identifier 10.1109/ACCESS.2023.3322959*

Driver-Pedestrian Interactions at Unsignalized

Crossings Are Not in Line With

the Nash Equilibrium

AMIR HOSSEIN KALANTARI , YUE YANG, YEE MUN LEE, NATASHA MERAT , AND GUSTAV MARKKULA

Institute for Transport Studies, University of Leeds, LS2 9JT Leeds, U.K. 

Corresponding author: Amir Hossein Kalantari \(a.h.kalantari@leeds.ac.uk\) This work was supported in part by the SHAPE-IT Project funded by the European Commission’s Horizon 2020 Framework Program under Grant 860410, and in part by the SHAPE-IT and HumanDrive Projects funded by Innovate UK and the Centre for Connected and Autonomous Vehicles \(TS/P012035/1\). 

This work involved human subjects or animals in its research. Approval of all ethical and experimental procedures and protocols was granted by the University of Leeds Ethics Committee, under Reference No. AREA 21-022. 

**ABSTRACT **Recent developments in vehicle automation require simulations of human-robot interactions in the road traffic context, which can be achieved by computational models of human behavior such as game theory. Game theory provides a good insight into road user behavior by considering agents’

interdependencies. However, it is still unclear whether conventional game theory is suitable for modeling vehicle-pedestrian interactions at unsignalized locations or if more complex models like behavioral game theory are needed. Hence, we compared four game-theoretic models based on two different payoff formulations and two solving algorithms, to answer this question. Unlike the most previous studies that employed naturalistic datasets to test and validate such models, this study utilized a distributed simulation dataset to test and compare the models. The study was conducted by connecting a CAVE-based pedestrian simulator to a motion-based driving simulator to replicate the traffic scenarios for 32 pedestrian-driver pairs. The findings demonstrated that there is a high variability between participant pairs’ behaviors. Our proposed behavioral game-theoretic model outperformed other models in predicting the interaction outcome. 

This translates to a decrease by 70% and 67% in the root mean squared error \(RMSE\) when compared to the baseline model, for marked and unmarked crossings, respectively. The model can also predict which interaction will take the longest time to resolve. According to our results, road users cannot be expected to behave in line with the Nash equilibrium of conventional game theory that underscores the complexity of human behavior with implications for the testing and development of automated vehicles. 

**INDEX TERMS **Psychology, mathematical models, human computer interaction, behavioral sciences, design for experiments. 

## **I. INTRODUCTION**

improvements in vehicle automation bringing the challenges Road user interaction has been a topic of interest for years of human-robot interaction into the topic \[2\], \[3\], \[4\]. Among

from a safety perspective for human-human interaction \[1\]

different types of interactions, the interaction of pedestrians and has become popular in recent years due to successive as vulnerable road users \(VRUs\) with drivers and automated vehicles \(AVs\) has a great impact on traffic safety and The associate editor coordinating the review of this manuscript and efficiency as pedestrians constitute a great proportion of approving it for publication was Jjun Cheng

. 

the traffic ecosystem \[5\]. They are also known to exhibit 2023 The Authors. This work is licensed under a Creative Commons Attribution 4.0 License. 

VOLUME 11, 2023

For more information, see https://creativecommons.org/licenses/by/4.0/

110707



A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings unpredictable behaviors \[6\]. To this end, previous research to be incorporated into other modeling approaches such as has strived to understand \[7\], \[8\], \[9\], \[10\] and quantitatively microscopic traffic flow models \[34\] and artificial neural model \[11\] how VRUs and vehicles/AVs interact with each networks \[35\] makes them an attractive choice. Having said other with the latter becoming an essential part of the test that, the discrete nature of these models provides no concept and development procedure for the future deployment of of time such as time-varying utility functions and the ability AVs \[12\]. 

to fully capture traffic agents’ interdependencies. To this end, The subsequent sections delve into the exploration of other modeling approaches such as evidence accumulation related work concerning the computational modeling of road and game theory have become popular for road user behavior user behavior. Subsequently, the methodology employed modeling studies, over recent years. 

in this study is explained, encompassing the empirical Evidence accumulation offers a well-established depiction investigation, computational models, and model fitting. 

of human behavior for some specific decisions \[36\], \[37\]

The results section provides a comparison of the distinct and suggests that evidence for a particular response is models developed within this study. The paper concludes by integrated by single or multiple accumulators over time discussing the findings and presenting the conclusions. 

and by a rate known as drift rate which is the rate at which sensory information reaches a bound \(a decision boundary\) \[23\]. This model has been used for simulating and A. RELATED WORK

predicting driver gap acceptance in left-turns \[38\], pedestrian

Existing modeling approaches to road user behavior are crossing decisions \[22\], \[39\], and AV-human interactions often separated into two types of architecture: glass-box in take-over and crossing scenarios \[40\]. That said, while and black-box models \[13\]. Black box models such as evidence accumulation models provide ample detail about the deep learning models offer a generalizable approach where decision-making process, they do so for a very constrained set the behavior of several agents can be simulated with high of tasks and are typically considered single-decision models accuracy \[14\] but the underlying mechanisms of the model suggesting they may not be able to account for all types components are unknown: there is a lack of interpretability of interaction scenarios. Also, as opposed to game-theoretic in the connection between the inputs and outputs of the models, these models are mostly incapable of capturing road model \[15\] and with human psychological theories which users’ interdependencies. 

makes the model interpretation difficult. On the other hand, Game theory extends optimal control theory to a decen-glass box models offer the advantage of interpretability and tralized multi-agent decision problem \[41\] and explains the transparency by providing explanations for the mechanisms interaction of multiple agents whose interests do not coincide, in relatively great detail. These models rely on differ-and their decisions, generally, depend on the actions of all ent modeling paradigms including agent-based modeling

\[42\]. In this model, agents keep revising their decisions and

\[16\], \[17\], optimal control theory \[18\], \[19\], Markovian beliefs until they become mutually consistent, that is until processes \[20\], \[21\], evidence accumulation \[22\], \[23\], 

\(the Nash\) equilibrium is reached. This is the core idea proxemics \[24\], discrete choice modeling \[25\], \[26\] and game in conventional \(also known as orthodox/traditional\) game theory \[27\]. 

theory which relies on perfect rationality of players who From the above modeling approaches, agent-based and dis-are always assumed to be self-interested and choose optimal crete choice models have a long and rich history in predicting choices. Overall, conventional game theory has the advantage road user behavior. Agent-based models have been used for of accounting for interdependencies, unlike agent-based, modeling different traffic scenarios such as two-dimensional logit, and evidence accumulation models \[43\]. Thus, it has trajectory modeling of vehicular movements at intersections been used in several vehicle-pedestrian interaction studies where one-dimensional simplification is not enough to

\[44\], \[45\], \[46\], \[47\], \[48\] However, behavioral economics capture road user behavior and distance-based factors play suggests that agents’ preferences, along with concern for a more important role than time-based variables \[28\]. The

fairness, are highly context-dependent \[49\]: individuals make downside of these models is that road users are generally decisions based on a heuristic estimate of the potential value assumed to act mostly like moving objects without consid-of losses and gains \[50\] and they do not usually play the ering each other’s intentions before making every decision. 

Nash equilibrium in strategic situations such as unrepeated Logit models are among the most commonly used models normal-form games \[51\]. This is due to different reasons, for modeling pedestrians’ gap acceptance behavior \[26\], \[29\], 

including bounded rationality \[52\], \[53\] and positive theory

\[30\], \[31\] due to the binary nature of pedestrian crossing deci-

\[54\] which are the backbones of behavioral game theory. 

sions, the convenience of utilizing them, and the flexibility of Behavioral game theory utilizes experimental evidence to their application together with other models \[32\]. They have create computational models of human cognitive limitations, been compared to a number of statistical methods namely social utility and preferences, and learning rules aware of maximum likelihood method, Raff’s method, root mean

‘‘ *how people actually behave in strategic situations*’’ \[55\]. 

square method and probability equilibrium method, and have To date, several behavioral game-theoretic models have been found to be the most appropriate model for estimating been introduced and tested using economic games. For the critical gaps of pedestrians \[33\]. Moreover, their ability instance, the dual accumulator \(DA\) model that combines the 110708

VOLUME 11, 2023



A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings knowledge of evidence accumulation paradigm with game simulation study, followed by a definition of each computa-theory is a promising approach to simulating human

tional model, and details of the model fitting. 

decision-making \[56\]. The authors compared their model to several existing behavioral game theory models, i.e., noisy A. EMPIRICAL STUDY

introspection \[57\], logit quantal response equilibrium \[58\], 

A distributed simulator study was conducted to inves-level-k reasoning \[53\], and cognitive hierarchy theory \[59\], 

tigate road user interactions in a safe and controlled employing a hold-one-out analysis. They showed that the environment, providing a large dataset of vehicle-pedestrian model makes the most accurate out-of-sample predictions interactive behaviors to test and validate the computational

\[56\]. However, this model has not previously been tested models of this study. The full details of the study can in the context of road user modeling, highlighting a gap in be found in \[67\]. Here, we provide a summary of the the literature. Some studies have employed other behavioral study. 

game theory models for the road traffic context, such as The study was conducted by connecting the University of the logit quantal response equilibrium in vehicle-pedestrian Leeds Driving Simulator \(UoLDS\) to the HIKER \(Highly interactions \[60\] and level-k reasoning \[61\], \[62\], \[63\] and

Immersive Kinematic Experimental Research\) pedestrian lab. 

cognitive hierarchy reasoning \[64\] in vehicle-vehicle \(includ-UoLDS is a high-fidelity motion-based driving simulator ing AVs\) interactions showing that the models can capture with an eight degree-of-freedom motion platform carrying road user behavior well. Using two different multiagent a Jaguar car housed in a 4 m-diameter spherical projection Markov-Games, i.e., one based on the Nash equilibrium and dome, with a 300◦ field-of-view projection system. HIKER is one based on logit quantal response equilibrium, Alsaleh a 9 × 4 m CAVE simulator consisting of eight 4k projectors and Sayed estimated cyclist-pedestrian strategies using a that are used to project virtual scenes at 120 Hz to the floor multiagent deep reinforcement learning approach and found and walls. Fourteen body markers were attached to different that the latter predicted road user trajectories with higher parts of the pedestrian’s body, represented as pink spheres accuracies \[65\]. 

to the driver \(Figure 1-a\). The pedestrian could also see the All things considered, to the best of our knowledge, vehicle as shown in Figure 1-b. 

no study has ever directly compared conventional game In this experiment, 64 participant pairs \(PPs\) \(32 drivers; theory to behavioral game theory in the vehicle-pedestrian Age: M = 31.53, R = 21−50, SD = 1.72\); paired with

interaction domain. Hence, it is currently unclear whether 32 pedestrians; Age: M = 25.09, R = 19−34, SD = 0.87\) conventional game theory models are sufficient for road user interacted with each other under different traffic scenarios. 

interaction and especially vehicle-pedestrian interactions, The study was approved by the University of Leeds Ethics or whether higher complexity in modeling provided by Committee \(Reference No AREA 21-022\). The scenarios behavioral game theory is needed. There is also a lack were defined based on different crossing types \(i.e., zebra of comparison between game-theoretic models and logit and non-zebra crossings; see Figure 1-c\) and five different models. The main contribution of this study is a comparison vehicle time-to-arrival conditions \(TTAs, i.e., the temporal of these two types of game theory models also with logit distance of the vehicle to the center of the crossing, 3−7 s\) models \(representing the popular modeling approach in this resulting in 10 conditions that were repeated two times in area\). This was done by using a dataset from a controlled each experimental block. There were two blocks resulting in distributed simulator study. Unlike naturalistic studies which 40 randomized trials per PP. 

are the common validation tools for the models of road user Upon arrival, both participants were asked to sit in their behavior \[66\], controlled studies provide a safe environment respective briefing areas in two separate rooms and read where one can directly control the interactions between and sign the consent form. The instruction to the pedestrian agents, varying the conditions of interest to study their causal was to stand at a marker on the HIKER’s floor \(the first \(rather than correlational\) impact on behaviors and outcomes. 

blue cross in Figure 1-c\) where they could see that cars Also, this technique enables multiple observations for each are going both ways but they could not tell when the participant, allowing a better understanding of interindividual subject vehicle was approaching due to a visual obstruction differences. 

\(a bus stop; Figure 1-c\). After hearing an auditory tone, Our main research question is as follows:

they were asked to step to a second marker which was the curb of the virtual road where the driver could see

- Are traditional models such as logit and conventional them. This marked the beginning of the interaction. The game theory \(the Nash equilibrium\) enough to predict participants \(driver and pedestrian\) could decide whether they vehicle-pedestrian interaction outcomes at unsignal-wanted to wait for the other to pass first or they themselves ized locations or are more complex models such as

passed. Both participants were told: ‘‘ *Please assume that* behavioral game theory needed? 

*you are late for an important meeting, such that you want* *to avoid any unnecessary delays, but of course, you also* **II. METHODOLOGY**

*want to stay safe*.’’ Drivers were told to maintain the speed This section describes all the methods used in the study, limit \(30 mph\) as they would in their normal driving and beginning with a description of the controlled distributed were also reminded that pedestrians have priority at zebra VOLUME 11, 2023

110709





A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **FIGURE 1. **\(a\) The driver’s view of the pedestrian: the driver is stopping, and the pedestrian is shown by pink spheres, \(b\) the pedestrian’s view of the vehicle in the pedestrian lab: the pedestrian is crossing the zebra and the subject vehicle is to their right and \(c\) top view of the zebra \(left\) and non-zebra crossing \(right\) in Unity including the designated standpoints \(blue markers\). 

crossings. Upon completion of the experiment, participants 2\) ORIGINAL CONVENTIONAL GAME-THEORETIC \(OCGT\)

were asked to fill out post-experiment questionnaires for MODEL

demographic information and personality traits \(not reported A conventional game theory model by Wu et al. which con-here, see \[67\]\). 

siders the two-agent game of vehicle-pedestrian was chosen and slightly modified \[48\]. This model was chosen due to a B. COMPUTATIONAL MODELS OF VEHICLE-PEDESTRIAN

well-balanced integration of road user safety and efficiency INTERACTION

metrics, the ease of working with its payoff formulation and 1\) LOGIT MODEL \(LOGIT\)

the fact that it is one of the few game-theoretic models in the A logistic model was tested assuming the utilities to be literature with an explicitly stated payoff formulation. The the linear function of TTA and pedestrians’ total waiting model was established as the baseline for comparison against time which is in line with the literature \[26\]. Two different other models utilizing more complex payoff formulations and intercepts were considered for each crossing:

solving algorithms. 

Table 1 shows the parameters of the study including the *U *= β0 *z*/ *nz *\+ β1TTA \+ β2WT

\(1\)

Wu et al. model’s parameters \[48\]. Table 2 shows the Wu et al. 

model’s payoff formulation. The model’s payoffs are defined as the probability of the pedestrian passing first or waiting as a summation of utilities relating to \(i\) the perceived risk of can be denoted by P\(U\) and P \(1 − U\) , respectively, the being involved in a conflict with another road user modeled as probability of pedestrian passing first can be defined using *k *= 1/TTA, and \(ii\) the time spent as a result of one waiting the Logit function \[26\]:

for another, which is equal to the time that the passer takes to pass the crossing \( *t*

1

*i*\). The presence of these utility values in P\(U\) =

\(2\)

all outcomes with a negative sign when they have a negative 1 \+ e−U

influence on a road user, or a positive sign otherwise, is the where ***U *** is the utility of waiting/passing for the pedestrian, main assumption of the formulation. Additionally, a weight β0 *z * and β *nz * are intercepts for the unmarked and marked coefficient was considered for the total waiting time of the crossings, respectively and β1 and β2 are coefficients for TTA pedestrians with the following assumption: pedestrians who and waiting time of pedestrians, respectively. 

have waited for a longer time, are more inclined to be cautious 110710

VOLUME 11, 2023



A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **TABLE 1. **Parameters of the study. 

**TABLE 2. **Wu et al. \[48\] Payoff matrix. \(The vehicle is the row player and 3\) ALTERNATIVE CONVENTIONAL GAME-THEORETIC

the pedestrian is the column player.\)

\(ACGT\) MODEL

An alternative payoff formulation was proposed, based on Wu et al.’s original payoff. The formulation was provided to correct some of the assumptions of the original payoff which we suspected did not correctly capture road users’

perceived utilities of the different outcomes. For instance, road users’ utility functions were modified to help the model distinguish between marked and unmarked crossings as and less likely to engage in risk-taking by accepting smaller shown in Table 3. According to traffic regulations in the U.K., gaps \[31\]. This was assumed in the opposite direction in the similar to many western European countries, drivers should original paper \[48\] as the authors’ definition of waiting time give way to pedestrians waiting to pass as well as those at a was different from our study. 

zebra crossing \(see Rule H2 in. The Official Highway Code, Table 2 suggests that there is no unique Nash equilibrium, 2023 \[69\]\). Thus, while based on the regulations pedestrians and the game has two dominant strategies \{\(pedestrian pass, have priority at a zebra crossing, the driver \(vehicle\) was also vehicle wait\), \(pedestrian wait, vehicle pass\)\} which can be assumed to have priority at non-zebra locations, as there was obtained using the mixed strategy algorithm by equating the no refuge for this crossing type and the crossing behavior expected utilities of each player \[68\]. 

could be considered as an instance of jaywalking \[70\] in the 2 *atv*

2 *atp*

experiment. 

*Ppp*, *Pvw*= \(

, 1 −

\)

\(3\)

2 *k *\+ \(1 \+ *c*\) *at*

The following modifications were made to the original *v*

2 *k *\+ \(1 \+ *c*\) *atp*

payoff formulations:

where *Ppp * and *Pvw * are the probability of pedestrian passing first and vehicle waiting, respectively \[48\]. Another

I\) The utility of risk perception is not considered when dominant strategy \( *Ppw*, *Pvp*\) can be obtained as one minus a road user is waiting for the other to pass first, thus the probabilities in \(3\). In this study, we present all the removing *k * from their utilities in these instances. 

results based on the pedestrian’s probability of passing II\) When road users with no right of way want to pass first. 

first, they get a higher negative score for risk perception VOLUME 11, 2023

110711



A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **TABLE 3. **Alternative payoff formulation. 

\( *knR*

\( *t*\)

*p*, *knRv * where *Rp *= 1 and *Rv *= 0 if pedestrians *e* λ \[

*VD*, *cD*

*P*

\( *t*\) =

\(8\)

have right of way \(i.e., at zebra crossings\), and vice *D*, *cD*

P

*e* λ \[

*VD*, *c *\( *t*\)

*D*

versa\). 

*c*

III\) When a road user waits for the other to pass first, *e* λ \[

*VP*, *w *\( *t*\)

*P*

*P*

\( *t*\) =

\(9\)

they do not only lose the approaching vehicle’s TTA *P*, *wP*

P

*e* λ \[

*VP*, *w *\( *t*\)

*P*

but also the pedestrians’ estimated crossing duration *w*

\[− *a*\( *tv *\+ *tp*\)\]. 

IV\) When a road user waits for the other to pass but where \[

*VD*, *c *\( *t*\) and \[

*V*

\( *t*\) are the values of action

*D*

*P*, *wP*

none of them passes immediately, they will lose their *c *= *cross * for driver and action *w *= *wait * for pedestrian, own passing time with a multiplier \( *m*\) which can respectively. *PD*, *c *\( *t*\) and *P*

\( *t*\) are the estimated action

*D*

*P*, *wP*

make it worse than waiting for the other to pass

probabilities for *c * and *w*, respectively and finally *vD*, *cD*, *cP*

first. 

\(value for driver of action *c * if pedestrian plays *c*\) and V\) When a vehicle waits for a pedestrian, the pedestrian *vP*, *w*

\(value for pedestrian of action *w * if driver plays *P*, *wD*

gains the vehicle’s TTA \( *t*

*w*\) are the payoffs as defined in the two-agent game under *v*\) instead of their crossing

duration \( *t*

study. By increasing λ , agents are more likely to choose *p*\). 

the option with the highest value whereas the lower values Similar to the original model, the above formulation was of this parameter represent agents with a greater degree of solved using the mixed-strategy Nash equilibrium and

‘‘randomness’’ in their decisions. 

\(4\) and \(5\) show pedestrians’ and vehicles’ probabilities of The model was slightly modified and named the general-passing first and waiting for zebra and non-zebra crossings, ized DA model. To this end, a distinction mechanism was respectively. 

added to the model which explains how rapidly activations and beliefs are updated by an agent, and how long it *a*\( *tv *\+ *mtv*\)− *kn*

*a*\( *tv *\+ *mtp*\)\+ *k*

*Pppz*, *Pvwz *= \(

,1−

\)

\(4\)

takes to perform such an update. This was done by setting *a*\( *ctv *− *tp *\+ *mtv*\)

2 *k *\+ *a*\( *ctp *\+ *mtp *− *tp*\) the parameters \(ω and γ in \(6\) and \(7\)\) that define the *a*\( *t *\+ *mtv*\)\+ *k*

*a*\( *t *\+

*v*

*mtp*\)− *kn*

*P*

*v*

rate of change during an update of the agents’ activations *ppnz*, *Pvwnz *= \(

,1−

\) \(5\)

2 *k *\+ *a*\( *ctv *− *tp *\+ *mtv*\) *a*\( *ctp*\+ *mtp *− *tp*\)

\(preferences\) and beliefs as follows: ω = 1 − γ whereas in the original DA model, it was assumed that ω = γ = 1. 

4\) BEHAVIORAL GAME-THEORETIC MODELS

Both ω and λ parameters are called ‘‘DA parameters’’ in Both original and alternative payoff formulations were this paper. Also, while in the original model, the first agent solved using a model from the behavioral game theory \(driver\) samples one of the other second agent’s \(pedestrian’s\) category creating OBGT \[original \(solved by\) behavioral actions *w * with probabilities *Pw * at each time step, and updates game theory\] and ABGT \[alternative \(solved by\) behavioral their own value based on that sample, a weighted average game theory\] models, respectively. The DA model from across all possible actions *w * is taken in the generalized model. 

the behavioral game theory category was chosen \[56\] and

This is also true for the other agents’ possible actions. 

utilized as an alternative game solution to the mixed-strategy The model has a concept of decision-making over time. 

Nash equilibrium. According to the model, agents gener-This time is known as model convergence time. The criterion ate preferences by considering the conveniently available for the convergence was to consider a threshold of 0.001 for strategies with assumptions about opponents’ preferred the change in the two consecutive probabilities of actions for strategies using evidence and stochastic sampling, i.e., both agents. 

the process of a finite number of accumulation steps in Figure 2 illustrates how road users decide whether to pass payoffs inspired by existing cognitive models of preferential first or wait for each other using the DA model under the choice \[56\]. 

following conditions: a\) *tv *= 6 *s*, *t *= 30 *s * and at a zebra The following equations show the model formulation: crossing and b\) *tv *= 5 *s*, *t *= 45 *s * and at a non-zebra crossing. As can be seen from the figure, the model assumes

\[

*V*

that both the driver’s and pedestrian’s values of actions are *D*, *c *\( *t *\) = γ \[

*V*

\( *t *− 1\)\+ω X *P*

\( *t *− 1\) *v*

\(6\)

*D*

*D*, *cD*

*P*, *w*

*D*, *c*

*w*

*P*

*D*, *cP*

the same at the first time step \(Figure 2-a\) as time goes

\[

*VP*, *w *\( *t*\) = γ \[

*V*

\( *t *− 1\)\+ω X *P*

\( *t *− 1\) *v*

\(7\)

*P*

*P*, *wP*

*D*, *c*

*P*, *w*

by, the value of passing first for the driver becomes lower *c*

*D*

*P*, *wD*

110712

VOLUME 11, 2023





A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **FIGURE 2. **An illustration of how the DA model works providing the estimated value and probability of pass/wait of both agents when the pedestrian passed first \(a\) and when they wait for the driver to pass first \(b\). The vertical dashed lines show the time that model converged according to the defined threshold. 

while it increases for the pedestrian. This happens because b\) Fixing DA parameters, i.e. choosing two constant both agents’ information about the priority rules and available values for λ representing high = 1 and low randomness =

safety margin is being updated over time. As a matter of this 18 and a predefined value \(i.e., 0.9\) for ω \[56\], and using deliberation process, the probability of passing first for the payoff parameters as free parameters, separate per participant pedestrian increases and converges to a constant value. The pair. 

opposite of this situation happens to the driver. Figure 2-b

c\) Having DA parameters shared across all participants shows the alternative, although with a slight difference, just and letting the payoff parameters be free per participant pair; after the first time step and at the beginning the values of both in this method, alternating minimization \[71\] was used to actions for the driver \(pass, yield\) tend to decrease and as a account for varying payoff \(free\) parameters with shared result, the probability of yielding to the pedestrian becomes DA model parameters across the PPs with the following higher. However, quite soon the probabilities of actions swap form:

places and the driver decides to pass first probably when observing the pedestrian is less assertive in crossing the road. 

maxθ

LL\(θ

PO,θDA

**PO**, θ **DA**\)

\(12\)

This happens because the pedestrian feels less safe at an where LL\(θ**PO**, θ**DA**\) is the total negative log-likelihood unmarked crossing although the safety margin seems to be function, θ**PO **is the vector of payoff parameters and θ**DA **is enough for them to pass first. 

the DA model parameters. This method solves the problem by fixing θ**PO **and minimizing in θ**DA**, and then fixing θ**DA** 5\) MODEL FIT

and minimizing in θ**PO**. 

All the models were fitted to the experiment dataset This method helps the function converge to a global using maximum likelihood estimation method by computing minimizer, which in our case is the total \(sum of\) negative likelihood and log-likelihood functions as follows: log-likelihood across all PPs. 

 *p*\( *X*

All models were fitted to both crossing locations at the



*ij*,θ \)

If the pedestrian *i * crossed



same time and thus the parameters were shared between the Lij =

in trial *j*

\(10\)

two crossing types. The above procedure was used for all



 1 − *p*\( *Xij*,θ \) Otherwise

models using Powell’s method implemented in Scipy \[72\]. 

X *n*

X *m*

*LL*\(θ\) =

log *L*

Table 6 shows the parameter ranges of all game-theoretic *ij*

\(11\)

*i*=1

*j*=1

models used in the study. The parameter space was chosen where *n *= 32 is the number of PPs and *p * is the in a way that guaranteed the best fit for each model after model-predicted probability of the pedestrian crossing first several rounds of manual testing regarding the optimization in trial *j * of participant *i*, where *Xij * specifies the experimental algorithm. The parameter bound criterion for all models condition on that trial, given model parameters θ. 

was to conform with the theoretical reasoning, for example, Both DA models \(i.e., ABGT and OBGT\) were fitted with by limiting the lower bounds of multipliers \( ***c***, ***m ***& ***n***\) to three different assumptions about the parameters:

1 or keeping ***a *** and δ between 0 and 1. The main criterion a\) Using both DA parameters \(i.e., ω, λ \) and the game-for choosing the bounds for the conventional game-theoretic theoretic model’s payoff parameters as free parameters, models was to discard any parametrization that yields separate per participant pair. 

probabilities outside the range of 0−1. Also, for all models, VOLUME 11, 2023

110713



A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings the bounds were set in a way that expanding them makes the and error indices \(MAE, RMSE\). However, when Wu et al.’s algorithm choose values resulting in a worse fit. 

payoff formulation was solved with the DA model \(OBGT\), All the models were compared using information loss a clear improvement can be seen in all cases, according to the criteria, i.e., the Akaike Information Criterion \(AIC\) and plots in Figure 3 and Table 4. Also, the logit model did a better the Bayesian Information Criterion \(BIC\), as well as error job of capturing pedestrians’ crossing behavior than ACGT, indicators, including the Mean Absolute Error \(MAE\) and the OBGT, and OCGT models but was outperformed by our

Root Mean Squared Error \(RMSE\). The following equations proposed model \(ABGT\) in almost all cases. The exceptional show the formulations for these metrics:

performance of the ABGT model is evident in the plots of PPs 2, 13, 14, 15, 20, 24, 25, 27, and 31. 

*AIC *= 2 *k *− 2 *ln*\(LL\(θ ***PO***, θ ***DA***\)\) \(13\)

Figure 4 and Table 4 show that similar to the zebra where k is the number of estimated parameters in the model. 

crossing, overall, the Wu et al. model combined with the DA model, i.e., OBGT, performed better than the baseline *BIC *= *kln*\( *n*\) − 2 *ln*\(LL\(θ ***PO***, θ ***DA***\)\) \(14\)

model \(OCGT\) but the differences were subtle for the non-zebra crossing. Also, the logit model performed second-best where: n is the sample size. 

with a weaker performance compared to the zebra crossing. 

1 X *n*

Unlike zebra crossing, the differences between the ACGT and *MAE *=

| *actual *− *predicted *|

\(15\)

*n*

*i*=1

ABGT are much more obvious. Although the two models where: |actual - predicted| is the absolute difference between utilize the exact same payoff formulations, the ABGT model the actual and predicted probabilities and n is the number of outperformed all other models in almost all cases while it data points. 

is clear that the ACGT model was not capable of exhibiting the observed pattern of probabilities. For ABGT, the model’s r 1 X *n*

capability to capture the more complex crossing behaviors of *RMSE *=

\( *actual *− *predicted *\)2

\(16\)

*n*

*i*=1

pedestrians No 3, 6, 8, 13, 14, 18, 19, 27 and 30 is specifically noticeable compared to other models. In addition, this model **III. RESULTS**

achieved a 70% reduction in RMSE for marked crossings and In this section, first, the observed behaviors of participant a 67% reduction for unmarked crossings when compared to pairs at both crossings are presented followed by the the baseline \(OCGT\) model. However, It is worth noting that modeling results for the individual and aggregated data. 

comparing models with varying numbers of free parameters should encompass both elements of model parsimony such A. OBSERVED BEHAVIOR AT BOTH CROSSINGS

as AIC, BIC, etc., and error indices. One cannot assert that Figures 3 and 4 show the crossing behavior as well as the a model is superior solely based on its predictive accuracy. 

probability of pedestrian crossing first as a function of time Overall, Table 4 shows that when moving from conven-gap, for all 32 PPs, for all models. Looking at the panels tional to behavioral game-theoretic models, the improve-in Figure 3, it can be seen that while different PPs behaved ments in all criteria, including negative log-likelihood differently for TTAs equal to two and three seconds, all of are observable which firmly confirms the observations of them passed the crossing first at higher time gaps. Also, Figure 3 and 4. 

28% \(nine out of 32\) of the pedestrians crossed first in all trials, irrespective of the available safety margin \(TTA\). 

C. OVERALL RESULTS FOR BOTH CROSSING TYPES

Looking at the observed data in Figure 4, one can see the Figure 5 shows the average of all 32 pedestrians’ crossing crossing behavior at non-zebra was quite different compared probabilities over time gaps for both crossing types. In line to the zebra crossing among the pedestrians: First, very few with the individual data, the overall fine performance of the pedestrians passed before the driver, at the 2-second TTA \(i.e., ABGT model and the better performance of the Wu et al. 

11, 12, and 29\). Second, the crossing probability increased combined with the DA model \(OBGT\) compared to the

for the 3-second time gaps but was still low. This was due original model \(OCGT\) is evident for both crossing types. 

to the crossing behavior of PP 3, 11, 12, 20, 23, 24, and 29. 

Third, data of some pedestrians, i.e., 17, 20, and 22 showed D. ABGT MODEL DECISION TIME

fluctuations \(rises and dips\) as TTA increased. Finally, three As explained in Figure 2, the dual accumulation process out of 32 pedestrians \(i.e., PPs 4, 25, and 28\) did not pass at in the DA model corresponds to a deliberation process all, suggesting they were risk-averse. 

that unfolds over time such that we can define a model convergence/decision time. Thus, we conducted a correlation B. MODEL PERFORMANCE FOR BOTH CROSSINGS

test to understand if there is a relationship between the Figure 3 shows that the two conventional game-theoretic ABGT model’s decision time \(DT\) and pedestrians’ crossing models, i.e., ACGT and OCGT performed comparatively initiation time \(CIT\) in the experiment \(i.e., from the time the weakly in almost all cases. This can be confirmed by looking auditory tone was triggered to the time the pedestrian started at Table 4 which shows the model comparison for both crossing the road, minus one second\). Table 5 shows that crossing types including information loss criteria \(AIC, BIC\) there is a weak, yet significant correlation \(r\(821\) = .213, 110714

VOLUME 11, 2023





A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **FIGURE 3. **Pedestrian’s probability of crossing first over time gap at zebra crossings for all models. 

VOLUME 11, 2023

110715





A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **FIGURE 4. **Pedestrian’s probability of crossing first over time gap at non-zebra crossings for all models. 

110716

VOLUME 11, 2023





A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **TABLE 4. **Model comparison. 

**FIGURE 5. **Average probability of pedestrian crossing first over time gap for all models. 

p = .000\), between the ABGT model’s DT and CIT, which **TABLE 5. **Correlation between ABGT’s DT and CIT. 

can be also confirmed by Figure 6. From the figure, it can be seen that most of the initiation times are concentrated in the 1−2 second range. The figure also shows that the model had a hard time predicting DT within this range. By increasing CIT, more instances of successful estimations are observable. 

Three different points were chosen to show how the model predicted the interaction outcome over time which can be seen by the respective insets. Figure 6 shows that in points C: point refers to PP 1 at non-zebra, with a TTA of 4 s, with a

\[1.5,290\] and B: \[5,490\] the model performed well. Point C

female driver and male pedestrian, and a waiting time of 64 s. 

belongs to PP 29 with the following experimental conditions: Although both the TTA and crossing type made the model non-zebra, TTA of 6 *s*, both female and the waiting time of predict lower values and subsequently lower probabilities 80 s and point B is for PP 8 at zebra, with a TTA of 5 s, with of passing first for the pedestrian over time, the pedestrian a male driver and female pedestrian, and a waiting time of passed first suggesting that there might be other influencing 78 s. Hence, probably the most obvious difference between factors such as gender and personality traits that were not these two points is the crossing type that led to different CITs considered for calculating the probabilities. 

and DTs. Finally, in point A: \[1.2, 895\], it can be seen that the pedestrian’s probability of passing and waiting swapped E. ABGT MODEL PARAMETERIZATION RESULTS

places after a few time steps which made the model predict the Figure 7 shows the pairwise distribution of the best-fitted interaction outcome incorrectly, and over a longer time. This model, i.e., ABGT parameterization as a function of the VOLUME 11, 2023

110717





A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **TABLE 6. **Parameter ranges for all GAME-THEORETIC models. 

**FIGURE 6. **The relationship between the ABGT model’s DT and CIT in the experiment. 

average probability of pedestrian crossing first in each PP. 

broadening the bounds did not result in a better model Thus, each point in the figure is representative of a PP. 

fit. 

From the figure, it can be seen that there is a positive correlation between the values of ***a *** and the average crossing **IV. DISCUSSION**

probability suggesting that higher values of this parameter In this study, we compared a number of computational resulted in higher average probabilities. Also, a moderate models of road user interaction, namely a logit model and negative correlation can be seen between ***a *** and ***c *** suggesting four game-theoretic models, using a controlled study. The that fixing one parameter \(e.g., ***a***\) and leaving the other findings showed that our proposed model, which was based one to vary freely could improve the model fit results. 

on behavioral game theory outperformed all others for almost However, it is quite debatable what would be the exact all PPs’ data, for both crossing types. The second-best value of the fixed parameter as there is no theoretical performing model was the Logit model confirming the reasoning for choosing a specific value for either of these findings of many studies that relied on this type of modeling parameters. One can try different values and see which to predict vehicle-pedestrian interaction outcomes \[26\], \[33\], 

value would yield the best results. Finally, several instances

\[73\]. Moreover, a huge improvement was observed by of hitting bounds can be seen but as we explained above, switching from mixed-strategy Nash equilibrium to dual 110718

VOLUME 11, 2023





A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings **FIGURE 7. **Pairwise distributions of parameters for ABGT model as a function of average crossing probability in each PP. 

accumulation to solve the same payoff matrices. This was librium’s inability to consider suboptimal road user behavior. 

especially noticeable for our ACGT versus ABGT models While one could argue that the performance difference and for the non-zebra crossing which constituted the worst between ACGT and ABGT models can be attenuated by

and the best models for this crossing type, respectively. 

formulating a different payoff matrix, we tend to believe that This helps us answer our main research question: In line it is less possible to propose a model based on a different with behavioral economics, people do not play the Nash payoff formulation and solve it by mixed-strategy algorithms, equilibrium in their daily life \[51\], which may also be true which works better than the ABGT model. This is due to about road users. As stated by \[74\], people are usually not the inherent limitation of the mixed-strategy algorithm with aware that they are playing a game. They have some beliefs respect to only considering the opposing player’s utilities. 

about their surroundings, other potential players and their Overall, the results of this study can be beneficial for the available strategies, and the possible outcomes of each chosen testing and development of AVs when there is a need for strategy. Hence, they use heuristics and the rule of thumb to studying a large number of vehicle-pedestrian interactions take action. Road users’ divergence from Nash equilibrium in a safe and controlled manner with subsequent computer has been reported in cyclist-pedestrian interactions \[65\] and

simulations and mathematical modeling. 

is observed here for vehicle-pedestrian interactions. \[65\]

Unlike other models used in the study, the behavioral suggested that this might be due to the possible Nash equi-game-theoretic models provide a concept of time and suggest VOLUME 11, 2023

110719



A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings that the initial conditions \(i.e., kinematics and crossing type\) aspects that still make the naturalistic data a necessary tool are processed over time. The time it takes for the model for a successful traffic microsimulation. 

to process those initial conditions correlates with the actual Another strength of this modeling approach is that the time it takes for the PPs to reach a point where one of the inputs of the proposed model \(the agents’ kinematics\) are agents can go ahead and pass first \(Figure 6\). That said, the usually easy to record and extract and unlike many models, agents may be adjusting their behavior at multiple points in it does not demand metrics such as vehicle’s deceleration, time during the interaction. Hence, the key simplification dimensions, etc. which are usually more difficult to achieve in the model is that the interaction is modeled as a single when using naturalistic video data. Moreover, while the mod-decision-making process making it a simple model capable of eling framework of this study is both computationally less predicting interaction outcomes, which could be quite useful expensive and intensive than most machine-learned models, in some types of applications. Also, the DA model relaxes we do not consider it quite a substitute for these black box this single decision simplification a little more, as there can models, rather, we think the combination of these two would be many steps of deliberation in the DA process, even though generate an even more powerful computational framework those steps of deliberation in the model are not connected to which balances interpretability and generalizability. 

how the external world is developing over time. 

Several improvements can be made to this study. First Moreover, checking the participant features and traffic and considering the empirical study, we did not account for conditions of the three selected points in Figure 6 revealed the interaction approach phase while research showed that that there was a difference in traffic conditions between the interaction commences as soon as road users see each the points where the model performed well \(i.e., **B **and other even before the time pedestrians reached the curb \[79\]. 

**C **in Figure 6\); longer CIT and DT were observed at a Second, making the utility functions time-varying would zebra crossing \(B\) compared to a non-zebra crossing \(C\). 

yield a more complete picture of the whole interaction from We have previously shown that pedestrians had considerably the approach phase to the time that both agents passed the longer CITs at zebra crossings in the experiment \[67\]. 

crossing. Third, from both the experimental and modeling Also, investigating the third point, i.e., **A**, where the model perspective, there is a need to further develop a method-performed poorly suggested that other factors such as ology to consider situations where multiple pedestrians are personality traits could play a role in the pedestrian’s CIT

interacting with multiple vehicles. This could be done by \(see \[67\]\). Therefore, the observed discrepancy between the using head-mounted displays where several pedestrians wear model’s DT prediction and the pedestrians’ CIT could be these devices connected over a network. Fourth, our ABGT

due to the lack of consideration of such variables. A more model currently uses some of the features of behavioral complete account of this negotiation process could include game theory while there are more aspects associated with these variables \(e.g., personality traits\) in future studies. 

this theory that distinguishes itself from its conventional We used a novel approach in model fitting employing counterpart concerning collective behavior, which have not a distributed simulation dataset to test and validate the been investigated in a road traffic setting. These include models. The controlled nature of the study allowed us theories of strategic complementarity \[52\], theories of team to understand and pinpoint each and every PP behavior, reasoning \[80\], and theories of social projection \[81\], \[82\]. 

individually as well as evaluate each model’s performance To this end, extending the framework to a multi-agent with respect to the individual data, something that is not problem is one of the most important future research possible in naturalistic studies. It also helped us formulate directions. Finally, due to the nature of the experimental the alternative payoff matrix having the confidence that work, the behavior of a limited number of people was there are no unknown correlations between the studied studied and the models’ performance including the proposed variables. Previously, we showed that distributed simulation ABGT model was judged accordingly. Future studies should can generate pedestrians’ gap acceptance behaviors, using test and validate the framework using large naturalistic a desktop driving simulator connected to the HIKER lab datasets to both confirm and improve its performance and

\[75\]. This paper tried to a take step forward in this direction generalizability. 

by replicating game-theoretic interactions using two high fidelity simulators to maximize the validity of the experiment. 

## **V. CONCLUSION**

That said, naturalistic data still provide some advantages over In this study, we compared several computational models simulator data which should not be overlooked: studying road of road user interaction using data from an experimental user behavior over a longer period to understand, for example, setting. The results showed that drivers and pedestrians do not driving patterns \[76\], giving a truthful representation of road play the Nash equilibrium when interacting at unsignalized users’ 2D movement on the road for vehicle-vehicle \[28\]

crossings and more complex behavioral modeling paradigms and vehicle-pedestrian interactions \[77\] and the capability of like behavioral game theory are needed to fully capture tracking a large number of road user parameters, especially the pedestrians crossing decisions at these locations. The those related to driving performance \[78\] are some of the ABGT model was successful in replicating these interactions 110720

VOLUME 11, 2023



A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings by taking into account how agents negotiate their available

\[16\] E. Bonabeau, ‘‘Agent-based modeling: Methods and techniques for strategies and gains and losses over time which sometimes simulating human systems,’’ *Proc. Nat. Acad. Sci. USA*, vol. 99, no. Suppl. 3, pp. 7280–7287, May 2002. 

results in choosing a suboptimal decision as opposed to the

\[17\] M. Prédhumeau, L. Mancheva, J. Dugdale, and A. Spalanzani, ‘‘Agent-assumed rationality of players in conventional game theory. 

based modeling for predicting pedestrian trajectories around an For instance, this model resulted in a reduction by 70%

autonomous vehicle,’’ *J. Artif. Intell. Res. *, vol. 73, pp. 1385–1433, Apr. 2022. 

and 67% in the RMSE compared to the OCGT model, for

\[18\] V.-A. Le and A. A. Malikopoulos, ‘‘A cooperative optimal control marked and unmarked crossings, respectively. These findings framework for connected and automated vehicles in mixed traffic using are especially a pivotal point for the virtual testing and social value orientation,’’ in *Proc. IEEE 61st Conf. Decis. Control \(CDC\)*, development of AVs where they need to take over human Dec. 2022, pp. 6272–6277. 

\[19\] I. M. Ross, *A Primer on Pontryagin’s Principle in Optimal Control*. Boston, driver tasks to a great extent taking the unpredictability MA, USA: Collegiate Publishers, 2015. 

of VRUs into account. That said, achieving this goal still

\[20\] R. Bellman, ‘‘A Markovian decision process,’’ *Indiana Univ. Math. J. *, requires significant progress, as discussed in the future vol. 6, no. 4, pp. 679–684, 1957. 

\[21\] Y.-C. Hsu, S. Gopalswamy, S. Saripalli, and D. A. Shell, ‘‘An MDP

research directions in the discussion. 

model of vehicle-pedestrian interaction at an unsignalized intersection,’’

in *Proc. IEEE 88th Veh. Technol. Conf. \(VTC-Fall\)*, Aug. 2018, **REFERENCES**

pp. 1–6. 

\[22\] J. Pekkanen, O. T. Giles, Y. M. Lee, R. Madigan, T. Daimon, N. Merat, 

\[1\] T. Bjørnskau and F. Sagberg, ‘‘Handling skills or improved road and G. Markkula, ‘‘Variable-drift diffusion models of pedestrian road-user interaction?’’ in *Traffic and Transport Psychology: Theory and* crossing decisions,’’ *Comput. Brain Behav. *, vol. 5, no. 1, pp. 60–80, *Application*. Amsterdam, The Netherlands: Elsevier, 2005, p. 129. 

Mar. 2022. 

\[2\] P. Koopman and M. Wagner, ‘‘Toward a framework for highly automated

\[23\] R. Ratcliff, P. L. Smith, S. D. Brown, and G. McKoon, ‘‘Diffusion decision vehicle safety validation,’’ SAE Tech. Paper 2018-01-1071, 2018, doi: model: Current issues and history,’’ *Trends Cogn. Sci. *, vol. 20, no. 4, 

10.4271/2018-01-1071. 

pp. 260–281, Apr. 2016. 

\[3\] G. Markkula, R. Madigan, D. Nathanael, E. Portouli, Y. M. Lee, 

\[24\] J. Domeyer, A. Dinparastdjadid, J. D. Lee, G. Douglas, A. Alsaid, A. Dietrich, J. Billington, A. Schieben, and N. Merat, ‘‘Defining interac-and M. Price, ‘‘Proxemics and kinesics in automated vehicle–pedestrian tions: A conceptual framework for understanding interactive behaviour in communication: Representing ethnographic observations,’’ *Transp. Res. *

human and automated road traffic,’’ *Theor. Issues Ergonom. Sci. *, vol. 21, *Rec. *, vol. 2673, no. 10, pp. 70–81, Oct. 2019. 

no. 6, pp. 728–752, Nov. 2020, doi: 10.1080/1463922X.2020.1736686. 

\[25\] D. A. Hensher and L. W. Johnson, *Applied Discrete-Choice Modelling*. 

\[4\] A. Turnwald and D. Wollherr, ‘‘Human-like motion planning based on Evanston, IL, USA: Routledge, 2018. 

game theoretic decision making,’’ *Int. J. Social Robot. *, vol. 11, no. 1, 

\[26\] J. Zhao, J. O. Malenje, Y. Tang, and Y. Han, ‘‘Gap acceptance probability pp. 151–170, Jan. 2019, doi: 10.1007/s12369-018-0487-2. 

model for pedestrians at unsignalized mid-block crosswalks based on

\[5\] World Health Organization. \(2013\). *Pedestrian Safety: A Road Safety* logistic regression,’’ *Accident Anal. Prevention*, vol. 129, pp. 76–83, *Manual for Decision-Makers and Practitioners*. \[Online\]. Available: Aug. 2019. 

https://apps.who.int/iris/rest/bitstreams/279316/retrieve

\[27\] R. Elvik, ‘‘A review of game-theoretic models of road user behaviour,’’

\[6\] B. C. de Lavalette, C. Tijus, S. Poitrenaud, C. Leproux, J. Bergeron, *Accid. Anal. Prev. *, vol. 62, pp. 388–396, Jan. 2014. 

and J.-P. Thouez, ‘‘Pedestrian crossing decision-making: A situational and

\[28\] J. Zhao, V. L. Knoop, and M. Wang, ‘‘Two-dimensional vehicular behavioral approach,’’ *Saf. Sci. *, vol. 47, no. 9, pp. 1248–1253, Nov. 2009, movement modelling at intersections based on optimal control,’’ *Transp. *

doi: 10.1016/j.ssci.2009.03.016. 

*Res. B, Methodol. *, vol. 138, pp. 1–22, Aug. 2020. 

\[7\] H. Amado, S. Ferreira, J. P. Tavares, P. Ribeiro, and E. Freitas, 

\[29\] D. B. Raghuram Kadali and D. P. Vedagiri, ‘‘Role of number of

‘‘Pedestrian–vehicle interaction at unsignalized crosswalks: A system-traffic lanes on pedestrian gap acceptance and risk taking behaviour at atic review,’’ *Sustainability*, vol. 12, no. 7, p. 2805, Apr. 2020, doi: uncontrolled crosswalk locations,’’ *J. Transp. Health*, vol. 19, Dec. 2020, 

10.3390/su12072805. 

Art. no. 100950. 

\[8\] R. E. Amini, C. Katrakazas, and C. Antoniou, ‘‘Negotiation and

\[30\] D. Sun, S. Ukkusuri, R. F. Benekohal, and S. T. Waller, ‘‘Modeling of decision-making for a pedestrian roadway crossing: A literature review,’’

motorist-pedestrian interaction at uncontrolled mid-block crosswalks,’’

*Sustainability*, vol. 11, no. 23, p. 6713, Nov. 2019. 

in *Proc. TRB Annu. Meeting CD-ROM*, Washington, DC, USA, 2003, 

\[9\] T. T. M. Tran, C. Parker, and M. Tomitsch, ‘‘A review of virtual reality pp. 1–34. 

studies on autonomous vehicle–pedestrian interaction,’’ *IEEE Trans. *

\[31\] G. Yannis, E. Papadimitriou, and A. Theofilatos, ‘‘Pedestrian gap *Human-Mach. Syst. *, vol. 51, no. 6, pp. 641–652, Dec. 2021. 

acceptance for mid-block street crossing,’’ *Transp. Planning Technol. *, 

\[10\] W. Wang, L. Wang, C. Zhang, C. Liu, and L. Sun, ‘‘Social interactions for vol. 36, no. 5, pp. 450–462, Jul. 2013. 

autonomous driving: A review and perspectives,’’ *Found. Trends Robot. *, 

\[32\] E. Papadimitriou, G. Yannis, and J. Golias, ‘‘A critical assessment of vol. 10, nos. 3–4, pp. 198–376, 2022. 

pedestrian behaviour models,’’ *Transp. Res. F, Traffic Psychol. Behaviour*, 

\[11\] F. Camara, N. Bellotto, S. Cosar, F. Weber, D. Nathanael, M. Althoff, J. Wu, vol. 12, no. 3, pp. 242–255, May 2009. 

J. Ruenz, A. Dietrich, G. Markkula, A. Schieben, F. Tango, N. Merat, and

\[33\] V. S. Vinayaraj, S. Arkatkar, G. Joshi, and M. Parida, ‘‘Examining C. Fox, ‘‘Pedestrian models for autonomous driving—Part II: High-level pedestrian critical gap analysis at un-signalized midblock crosswalk models of human behavior,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 22, sections in India,’’ *Transp. Res. Proc. *, vol. 48, pp. 2230–2250, 2020. 

no. 9, pp. 5453–5472, Sep. 2021. 

\[34\] J. Zhao, J. O. Malenje, J. Wu, and R. Ma, ‘‘Modeling the interaction

\[12\] G. Markkula and M. R. Dogar, ‘‘Models of human behavior for human–

between vehicle yielding and pedestrian crossing behavior at unsignalized robot interaction and automated driving: How accurate do the models of midblock crosswalks,’’ *Transp. Res. F, Traffic Psychol. Behaviour*, vol. 73, human behavior need to be?’’ *IEEE Robot. Autom. Mag. *, early access, pp. 222–235, Aug. 2020. 

Aug. 8, 2022, doi: 10.1109/MRA.2022.3182892. 

\[35\] B. R. Kadali, P. Vedagiri, and N. Rathi, ‘‘Models for pedestrian gap

\[13\] A. Rai, ‘‘Explainable AI: From black box to glass box,’’ *J. Acad. Marketing* acceptance behaviour analysis at unprotected mid-block crosswalks under *Sci. *, vol. 48, no. 1, pp. 137–141, Jan. 2020. 

mixed traffic conditions,’’ *Transp. Res. F, Traffic Psychol. Behaviour*, 

\[14\] S. Mozaffari, O. Y. Al-Jarrah, M. Dianati, P. Jennings, and A. Mouzakitis, vol. 32, pp. 114–126, Jul. 2015. 

‘‘Deep learning-based vehicle behavior prediction for autonomous driving

\[36\] G. Markkula, Z. Uludağ, R. M. Wilkie, and J. Billington, ‘‘Accumulation applications: A review,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 23, no. 1, of continuously time-varying sensory evidence constrains neural and pp. 33–47, Jan. 2022. 

behavioral responses in human collision threat detection,’’ *PLoS Comput. *

\[15\] L. H. Gilpin, D. Bau, B. Z. Yuan, A. Bajwa, M. Specter, and L. Kagal, *Biol. *, vol. 17, no. 7, Jul. 2021, Art. no. e1009096. 

‘‘Explaining explanations: An overview of interpretability of machine

\[37\] B. A. Purcell and T. J. Palmeri, ‘‘Relating accumulator model param-learning,’’ in *Proc. IEEE 5th Int. Conf. Data Sci. Adv. Anal. \(DSAA\)*, eters and neural dynamics,’’ *J. Math. Psychol. *, vol. 76, pp. 156–171, Oct. 2018, pp. 80–89. 

Feb. 2017. 

VOLUME 11, 2023

110721



A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings

\[38\] A. Zgonnikov, D. Abbink, and G. Markkula, ‘‘Should I stay or should I

\[62\] D. W. Oyler, Y. Yildiz, A. R. Girard, N. I. Li, and I. V. Kolmanovsky, go? Cognitive modeling of left-turn gap acceptance decisions in human

‘‘A game theoretical model of traffic with multiple interacting drivers for drivers,’’ *Human Factors*, Dec. 2022, Art. no. 001872082211445. 

use in autonomous vehicle development,’’ in *Proc. Amer. Control Conf. *

\[39\] O. Giles, G. Markkula, J. Pekkanen, N. Yokota, N. Matsunaga, N. Merat, *\(ACC\)*, Jul. 2016, pp. 1705–1710. 

and T. Daimon, ‘‘At the zebra crossing: Modelling complex decision

\[63\] S. Zhang, Y. Zhi, R. He, and J. Li, ‘‘Research on traffic vehicle behavior processes with variable-drift diffusion models,’’ in *Proc. 41st Annu. *

prediction method based on game theory and HMM,’’ *IEEE Access*, vol. 8, *Meeting Cogn. Sci. Soc. *, 2019, pp. 366–372. 

pp. 30210–30222, 2020. 

\[40\] G. Markkula, R. Romano, R. Madigan, C. W. Fox, O. T. Giles, and

\[64\] S. Li, N. Li, A. Girard, and I. Kolmanovsky, ‘‘Decision making in N. Merat, ‘‘Models of human decision-making as tools for estimating and dynamic and interactive environments based on cognitive hierarchy theory, optimizing impacts of vehicle automation,’’ *Transp. Res. Rec. *, vol. 2672, Bayesian inference, and predictive control,’’ in *Proc. IEEE 58th Conf. *

no. 37, pp. 153–163, Dec. 2018. 

*Decis. Control \(CDC\)*, Dec. 2019, pp. 2181–2187. 

\[41\] T. Başar and G. J. Olsder, *Dynamic Noncooperative Game Theory*. 

\[65\] R. Alsaleh and T. Sayed, ‘‘Do road users play Nash equilibrium? 

Philadelphia, PA, USA: SIAM, 1998. 

A comparison between Nash and logistic stochastic equilibriums for

\[42\] D. Novikov, V. Korepanov, and A. Chkhartishvili, ‘‘Reflexion in mathe-multiagent modeling of road user interactions in shared spaces,’’ *Expert* matical models of decision-making,’’ *Int. J. Parallel, Emergent Distrib. *

*Syst. Appl. *, vol. 205, Nov. 2022, Art. no. 117710. 

*Syst. *, vol. 33, no. 3, pp. 319–335, May 2018. 

\[66\] W. van Haperen, M. S. Riaz, S. Daniels, N. Saunier, T. Brijs, and G. Wets, 

\[43\] N. J. Evans and E.-J. Wagenmakers, ‘‘Evidence accumulation models:

‘‘Observing the observation of \(vulnerable\) road user behaviour and Current limitations and future directions,’’ *Quant. Methods Psychol. *, traffic safety: A scoping review,’’ *Accident Anal. Prevention*, vol. 123, vol. 16, no. 2, pp. 73–90, Apr. 2020. 

pp. 211–221, Feb. 2019. 

\[67\] A. H. Kalantari, Y. Yang, J. G. de Pedro, Y. M. Lee, A. Horrobin, 

\[44\] F. Camara, P. Dickinson, and C. Fox, ‘‘Evaluating pedestrian interaction A. Solernou, C. Holmes, N. Merat, and G. Markkula, ‘‘Who goes preferences with a game theoretic autonomous vehicle in virtual reality,’’

first? A distributed simulator study of vehicle–pedestrian interaction,’’

*Transp. Res. F, Traffic Psychol. Behaviour*, vol. 78, pp. 410–423, *Accident Anal. Prevention*, vol. 186, Jun. 2023, Art. no. 107050, doi: Apr. 2021. 

10.1016/j.aap.2023.107050. 

\[45\] C. W. Fox, F. Camara, G. Markkula, R. A. Romano, R. Madigan, and

\[68\] W. Spaniel, *Game Theory 101: The Complete Textbook*. Scotts Valley, CA, N. Merat, ‘‘When should the chicken cross the road? Game theory USA: CreateSpace, 2014. 

for autonomous vehicle–human interactions,’’ in *Proc. 4th Int. Conf. *

\[69\] Driving Standards Agency. \(2023\). *The Official Highway Code*. 

*Vehicle Technol. Intell. Transp. Syst. * Setúbal, Portugal: SciTePress, 2018, 

\[Online\]. Available: https://www.highwaycodeuk.co.uk/rules-for-pedestri-pp. 431–439. 

ans-crossings.html

\[46\] F. T. Johora and J. P. Müller, ‘‘Zone-specific interaction modeling of

\[70\] T. Wang, J. Wu, P. Zheng, and M. McDonald, ‘‘Study of pedestrians’

pedestrians and cars in shared spaces,’’ *Transp. Res. Proc. *, vol. 47, gap acceptance behavior when they jaywalk outside crossing facili-pp. 251–258, Jan. 2020. 

ties,’’ in *Proc. 13th Int. IEEE Conf. Intell. Transp. Syst. *, Sep. 2010, 

\[47\] H. Li, H. Hu, Z. Zhang, and Y. Zhang, ‘‘The role of yielding cameras in pp. 1295–1300. 

pedestrian-vehicle interactions at un-signalized crosswalks: An application

\[71\] I. Csiszár and G. Tusnady, ‘‘Information geometry and alternating of game theoretical model,’’ *Transp. Res. F, Traffic Psychol. Behaviour*, minimization procedures,’’ *Statist. Decisions*, vol. 1, no. 1, pp. 205–237, vol. 92, pp. 27–43, Jan. 2023. 

1984. 

\[48\] W. Wu, R. Chen, H. Jia, Y. Li, and Z. Liang, ‘‘Game theory

\[72\] P. Virtanen et al., ‘‘SciPy 1.0: Fundamental algorithms for scien-modeling for vehicle–pedestrian interactions and simulation based on tific computing in Python,’’ *Nature Methods*, vol. 17, pp. 261–272, cellular automata,’’ *Int. J. Mod. Phys. C*, vol. 30, no. 4, Apr. 2019, Feb. 2020. 

Art. no. 1950025. 

\[73\] Marisamynathan and V. Perumal, ‘‘Study on pedestrian crossing behavior

\[49\] C. F. Camerer, ‘‘Behavioural game theory,’’ in *Behavioural and Experi-at signalized intersections,’’ J. Traffic Transp. Eng. English Ed. , vol. 1, mental Economics. London, Springer, 2010, pp. 42–50. *
* 
no. 2, pp. 103–110, Apr. 2014. 

\[50\] D. Kahneman and A. Tversky, ‘‘Prospect theory: An analysis of decision

\[74\] G. J. Mailath, ‘‘Do people play Nash equilibrium? Lessons from under risk,’’ in Handbook of the Fundamentals of Financial Decision evolutionary game theory,’’ J. Econ. Literature, vol. 36, pp. 1347–1374, Making: Part I. Singapore: World Scientific, 2013, pp. 99–127. 

Sep. 1998. 

\[51\] J. R. Wright and K. Leyton-Brown, ‘‘Predicting human behavior in

\[75\] A. H. Kalantari, G. Markkula, C. Uzondu, W. Lv, J. G. de Pedro, unrepeated, simultaneous-move games,’’ Games Econ. Behav. , vol. 106, R. Madigan, Y. M. Lee, C. Holmes, and N. Merat, ‘‘Vehicle-pedestrian pp. 16–37, Nov. 2017. 

interactions at uncontrolled locations: Leveraging distributed simu-

\[52\] C. F. Camerer and E. Fehr, ‘‘When does ‘Economic Man’ dominate social lation to support game-theoretic modeling,’’ in Proc. Transp. Res. 

behavior?’’ Science, vol. 311, no. 5757, pp. 47–52, Jan. 2006. 

Board 101st Annu. Meeting, 2022, Paper no. TRBAM-22-01874, doi:

\[53\] D. O. Stahl and P. W. Wilson, ‘‘On players’ models of other players:

10.13140/RG.2.2.15469.72165. 

Theory and experimental evidence,’’ Games Econ. Behav. , vol. 10, no. 1, 

\[76\] J. Balsa-Barreiro, P. M. Valero-Mora, M. Menéndez, and R. Mehmood, pp. 218–254, Jul. 1995. 

‘‘Extraction of naturalistic driving patterns with geographic information

\[54\] A. M. Colman, ‘‘Cooperation, psychological game theory, and limitations systems,’’ Mobile Netw. Appl. , pp. 1–17, Oct. 2020. 

of rationality in social interaction,’’ Behav. Brain Sci. , vol. 26, no. 2, 

\[77\] F. Camara and C. Fox, ‘‘Space invaders: Pedestrian proxemic utility pp. 139–153, Apr. 2003. 

functions and trust zones for autonomous vehicle interactions,’’ Int. 

\[55\] C. F. Camerer, ‘‘Behavioural studies of strategic thinking in games,’’

J. Social Robot. , vol. 13, no. 8, pp. 1929–1949, Dec. 2021. 

Trends Cogn. Sci. , vol. 7, no. 5, pp. 225–231, May 2003. 

\[78\] J. Balsa-Barreiro, P. M. Valero-Mora, J. L. Berné-Valero, and

\[56\] R. Golman, S. Bhatia, and P. B. Kane, ‘‘The dual accumulator model of F.-A. Varela-García, ‘‘GIS mapping of driving behavior based on strategic deliberation and decision making,’’ Psychol. Rev. , vol. 127, no. 4, naturalistic driving data,’’ ISPRS Int. J. Geo-Inf. , vol. 8, no. 5, p. 226, pp. 477–504, Jul. 2020. 

May 2019. 

\[79\] A. Gorrini, L. Crociani, G. Vizzari, and S. Bandini, ‘‘Observation

\[57\] J. K. Goeree and C. A. Holt, ‘‘A model of noisy introspection,’’ Games results on pedestrian-vehicle interactions at non-signalized intersections Econ. Behav. , vol. 46, no. 2, pp. 365–382, Feb. 2004. 

towards simulation,’’ Transp. Res. F, Traffic Psychol. Behaviour, vol. 59, 

\[58\] R. D. McKelvey and T. R. Palfrey, ‘‘Quantal response equilibria for normal pp. 269–285, Nov. 2018. 

form games,’’ Games Econ. Behav. , vol. 10, no. 1, pp. 6–38, Jul. 1995. 

\[80\] A. M. Colman, B. D. Pulford, and C. L. Lawrence, ‘‘Explaining strategic

\[59\] C. F. Camerer, T.-H. Ho, and J.-K. Chong, ‘‘A cognitive hierarchy model coordination: Cognitive hierarchy theory, strong Stackelberg reasoning, of games,’’ Quart. J. Econ. , vol. 119, no. 3, pp. 861–898, Aug. 2004. 

and team reasoning,’’ Decision, vol. 1, no. 1, pp. 35–58, Jan. 2014. 

\[60\] Y. Zhang and J. D. Fricker, ‘‘Incorporating conflict risks in pedestrian-

\[81\] J. I. Krueger, ‘‘Methodological individualism in experimental games: motorist interactions: A game theoretical approach,’’ Accident Anal. 

Not so easily dismissed,’’ Acta Psychol. , vol. 128, no. 2, pp. 398–401, Prevention, vol. 159, Sep. 2021, Art. no. 106254. 

Jun. 2008. 

\[61\] B. M. Albaba and Y. Yildiz, ‘‘Driver modeling through deep reinforcement

\[82\] J. I. Krueger, T. E. Didonato, and D. Freestone, ‘‘Social projection learning and behavioral game theory,’’ IEEE Trans. Control Syst. Technol. , can solve social dilemmas,’’ Psychol. Inquiry, vol. 23, no. 1, pp. 1–27, vol. 30, no. 2, pp. 885–892, Mar. 2022. 

Jan. 2012. 

110722

VOLUME 11, 2023





A. H. Kalantari et al.: Driver-Pedestrian Interactions at Unsignalized Crossings AMIR HOSSEIN KALANTARI received the B.Sc. 

NATASHA MERAT received the Ph.D. degree

degree in civil engineering and the M.Sc. degree

in psychology, in 1999. She currently leads

in transport engineering, in 2015 and 2018, 

the Human Factors and Safety Group, Institute

respectively. He is currently pursuing the Ph.D. 

for Transport Studies, University of Leeds. Her

degree in transport studies with the University of

primary research interests include investigating

Leeds, U.K. He is also a Postdoctoral Research

the interactions between road users and novel

Fellow with TU Delft. In 2020, he was granted a

technologies. Specifically, she delves into the

Marie Skłodowska-Curie Actions Fellowship and

implications of driver impairment and distraction

joined the SHAPE-IT Project as an Early-Stage

and she is renowned globally as an expert in

Researcher. His research interests include traffic

studying the human factors of highly automated

psychology, road user behavior modeling, and studying the interaction of vehicles. She is also involved in six U.K. and European projects related autonomous vehicles with vulnerable road users. He has been a member of to automated vehicles. She is the Co-Chair of the TRB Sub-Committee on the American Society of Civil Engineers \(ASCE\), since 2015. 

Human Factors in Road Vehicle Automation, and a task leader of a tri-lateral working group on human factors of automation, leading activities between EU-U.S.-Japan. She has advisory board roles for Veoneer Inc., Highways England, the EC’s H2020 Transport Advisory Group, and Zenzic. 

YUE YANG received the B.Eng. degree in automa-

tion and control science from the Harbin Institute

of Technology, in 2017, and the M.Sc. degree

in human–computer interaction and design from

the KTH Royal Institute of Technology, in 2020. 

She is currently pursuing the Ph.D. degree with

the Institute for Transport Studies, University of

Leeds. She is also a Marie Curie Early Stage

Researcher with the Institute for Transport Studies, University of Leeds. Her research interests include human–machine interface, pedestrian behavior and crossing intent, and autonomous driving. 

YEE MUN LEE received the B.Sc. degree \(Hons.\)

in psychology and the Ph.D. degree in driving

GUSTAV MARKKULA received the M.Sc. degree

cognition from the University of Nottingham

in engineering physics and complex adaptive

Malaysia, in 2012 and 2016, respectively. She

systems and the Ph.D. degree in machine and

is currently a Senior Research Fellow with the

vehicle systems from the Chalmers University of

Institute for Transport Studies, University of

Technology, Gothenburg, Sweden, in 2004 and

Leeds. Her current research interests include

2015, respectively. He has more than a decade

investigating the interaction between automated

of research and development experience from the

vehicles and other road users, by using various

automotive industry. He is currently the Chair of

methods, especially virtual reality experimental

Applied Behavior Modeling with the Institute for

designs. She is also a Co-Lead of the User Sub-Project of an EU-funded Transport Studies, University of Leeds, U.K. His

project, Hi-Drive. Finally, she is one of the SHAPE-IT project supervisors, current research interests include the quantitative modeling of road user where she continues her research on human interaction with AVs in urban behavior and interaction, and the virtual testing of vehicle safety and scenarios, and also actively involved in the International Organization for automation technology. 

Standardization \(ISO\). 

VOLUME 11, 2023

110723


*



