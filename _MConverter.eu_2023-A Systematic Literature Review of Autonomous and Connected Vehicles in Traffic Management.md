***applied ***

***sciences***

Review

**A Systematic Literature Review of Autonomous and Connected**

**Vehicles in Traffic Management**

**Fayez Alanazi**

Civil Engineering Department, College of Engineering, Jouf University, Sakaka 72388, Saudi Arabia; fkalanazi@ju.edu.sa

**Abstract: **The emergence of autonomous vehicles and the advancement of technology over the past several decades has increased the demand for intelligent intersection management systems. Since there has been increased interest in researching how autonomous vehicles manage traffic at junctions, a thorough literature analysis is urgently needed. This study discovered peer-reviewed publications published between 2012 and 2022 in the most prestigious libraries to address this problem. After that, 100 primary studies were identified, and the chosen literature was subjected to systematic analysis. According to the findings, there are four primary categories of approaches, i.e., rule-based, optimization, hybrid, and machine learning procedures, which are used to achieve diverse driving objectives, including efficacy, safety, ecological, and passenger ease. The analyses illustrate the many attributes, limits, and views of the current solutions. This analysis enables the provision of potential future difficulties and directions in this study area. 

**Keywords: **autonomous vehicles; connected vehicles; intelligent transportation system \(ITS\); traffic management

**1. Introduction**

With population growth, there are more and more automobiles on the roadways. Peak hours in nearly all extensive metropolitan regions are incredibly congested. A simple **Citation: **Alanazi, F. A Systematic

road repair project or an unfortunate accident might cause a significant delay \[1\]. Each Literature Review of Autonomous

year, 1.35 million individuals lose their lives in traffic accidents \[2\]. Thus, traffic safety has and Connected Vehicles in Traffic

been one of the critical problems investigated in intelligent transportation systems \(ITS\), as Management. Appl. Sci. **2023**, 13, 

significant accidents entail the loss of life and devastation of infrastructures \[3\]. Fortunately, 1789. https://doi.org/10.3390/

cutting-edge information and communications technology have enabled notable safety

app13031789

features to be included \[4,5\]. As a result, driverless vehicles are a practical option that might improve road traffic flow while also increasing driving safety and trip comfort \[6\]. 

Academic Editors: Juan Li and

Bobin Wang

The Society of Automotive Engineers, generally termed as SAE, categorized autonomous vehicles \(AVs\) at levels 4 and 5—also known as self-driving vehicles—which can function Received: 29 December 2022

with no human intervention. 

Revised: 23 January 2023

In addition to being self-reliant, connected and autonomous vehicles \(CAVs\) can Accepted: 26 January 2023

interact with other nearby vehicles, the infrastructure, and even cloud services to share Published: 30 January 2023

data on the traffic and infrastructure \(such as the status of traffic signals or the existence of a downstream queue\) \[7\]. Although connected vehicles \(CVs\) may communicate with their surroundings, a human driver controls them. Due to the numerous potential sociological and financial advantages of autonomous driving, there has been a substantial increase in **Copyright:**

© 2023 by the author. 

research interest over the past two decades. Autonomous vehicles \(AVs\) promise lower Licensee MDPI, Basel, Switzerland. 

This article is an open access article

carbon emissions than conventional vehicles, while also enhancing the economy, efficiency, distributed under the terms and

and safety \[8\]. Unfortunately, making high-level decisions in AVs is difficult because of conditions of the Creative Commons

the complex and dynamic traffic environment, particularly in mixed traffic coexisting with Attribution \(CC BY\) license \(https://

other car drivers. Road intersections, interchanges, and roundabouts are particularly prone

creativecommons.org/licenses/by/

to accidents because collisions happen when two or more vehicles approach the exact 4.0/\). 

location simultaneously. 

Appl. Sci. **2023**, 13, 1789. https://doi.org/10.3390/app13031789

https://www.mdpi.com/journal/applsci

Appl. Sci. **2023**, 13, 1789

2 of 27

Intersections, interchanges, and roundabouts have been widely used in the traffic infrastructure to boost traffic safety, since they do so while also requiring less maintenance and higher traffic flow \[9\]. For these considerations, numerous researchers used a variety of traffic management strategies that were included in AVs and CVs to reduce the likelihood of accidents. Recently, the usage of blockchain technology has increased in the transportation sector \[10\]. Moreover, traditional Adaptive Cruise Control \(ACC\), Three-traffic-Phase Adaptive Cruise Control \(TPACC\), and others have been recently employed \[11\]. Therefore, it is essential to evaluate the literature already in existence, particularly those related to the methods used to control the application of autonomous vehicle traffic flow. This is crucial to map out pertinent articles and academic works in an organized manner to find the answers offered for AVs and CVs. 

This research paper aims to highlight existing research on the many types of AV and CV methodologies used in traffic management, along with suggested fixes and purposes methods to avoid junction conflicts, increase traffic harmonization, and reach environmental/social objectives. The goal is to offer a community-driven beginning for a better investigation of creating traffic management strategies that investigate suitable solutions regarding various traffic circumstances. To do this, the study will critically evaluate recent works and research on autonomous vehicles, using our observations to create innovative approaches. 

1.1. Prior Research

To the best of our knowledge, there do not seem to be many surveys and systematic literature reviews \(SLRs\) examining the various approaches autonomous vehicles use to control traffic at junctions. Even though different AV- and CV-related topics \[11–17\] have been the subject of several research studies, our study is distinct from those in terms of techniques, content, and research interests. Articles \[15–17\] summarized the methods used in traffic management systems to assess various traffic flow patterns and/or different types of crossings. Recently, a study document from 2022 primarily concerned with driverless vehicles’ environmental effects was published \[18\]. Our research thoroughly evaluated the scientific literature, extending the focus beyond air pollution to include water, land, noise, and light pollution. 

Only a small fraction of traffic management strategies has been examined in the above research, emphasizing one particular traffic scenario \(junction\) and a set of constrained driving goals. There is still room for more research and understanding in suggesting or advising acceptable procedures. To guide future research directions, it is essential to deliver a detailed summary of the most recent journal articles, specifically on traffic management strategies used by AVs and CVs at all three major traffic conflicts \(intersections, roundabouts, and interchanges\). The study examines and contrasts how well the ways are reviewed on the outcomes of the assessment. First, the goals of the methods were defined and classified, such as increasing efficiency and safety. The study, then, evaluated how effectively various strategies accomplished a specific objective. 

1.2. Research Goal

This research aims to review previous studies’ findings and provide a summary of how to manage traffic with autonomous and connected vehicles. Technical research questions were created in this section to help us concentrate on this matter, as shown in Table 1. 

**Table 1. **Research questions. 

**RQ1: **What driving objectives did traffic management studies consider while using AVs? 

**RQ2**: What traffic management techniques have been suggested to handle the possible issues brought on by AVs? 

**RQ3: **What concerns and issues in traffic management techniques still need to be resolved? 



*Appl. Sci. ***2023**, * 13*, x FOR PEER REVIEW 

3 of 28 



**RQ2**: What traffic management techniques have been suggested to handle the possible issues brought on by AVs? 

Appl. Sci. **2023**, 13, 1789**RQ3: **What concerns and issues in traffic management techniques still need to be resolved? ** **

3 of 27

*1.3. Contribution and Layout *

This S 1.3. 

LR Contribution

enhances ea

and

rlier Layout

research and adds the following to the work of those inter-

ested in traffic management using AVs in the disciplines of transport and computer sci-This SLR enhances earlier research and adds the following to the work of those inter-ence: 

ested in traffic management using AVs in the disciplines of transport and computer science:

• 

Throu •

gh eaThr

rly ough

Nove early

mber November

2022, 140 2022, 

critical 140

pa critical

pers on papers

connec on

ted connected

and autonoand

mo autonomous

us 

vehicle traf vehicle

fic man traf

age fic

m management

ent were dis wer

cover e discover

ed. This ed. 

wor This

k can work

be a fcan

ounbe

da ati foundation

on for fu-

for future, 

ture, more mor

in-d e

epin-depth

th scien scientific

tific studie studies

s in this in

a this

rea. area. 

• 

Then, •

100 siThen, 

gn

100

ificant significant

studies 

studies

were selec wer

ted e

tha selected

t adhere that

d to adher

our cr ed to

iteria our

for t criteria

he qua for

lity the quality

evaluation evaluation

stage. Wh stage. 

en com When

pared compar

to other ed

re to

sea other

rch of r

a esear

similch

ar of

sora similar

t, these i sort, 

nvest these

iga-

investiga-

tions can of tions

fer vacan

lua offer

ble davaluable

ta. 

data. 

• 

Then, •

the d Then, 

ata f

the

rom 1 data

00 resfrom

earch 100



resear

were care ch

f

wer

ully a e

nacar

lyzefully

ed, an analyzed, 

d data 

and

were o data

btain

wer

ed to e obtained

pinpoint 

to

con pinpoint

cepts and concepts

pro

and

blems re pr

la oblems

ted to d relat

esign ed

s fo to

r designs

AV and for

CV AV

traf and

fic CV

con traf

trol fic control

methods. methods. 

• 

In thi •

s rega In

rd, this

this r

egar

s

d, 

tudy thi

pro s study

vides a pr

m ovides

eta-ana a

ly meta-analysis

sis of traff

of

ic man traf

a

fic management

gement techniques techniques

and goals t and

o 

goals

enhance to

in enhance

telligent intelligent

transportatitransportation

on systems an systems

d emergi and

n

emer

g techn ging

ologietechnologies. 

s. 

• 

In add •

ition In

to addition

research to

ingr esear

diff ching

erent mdif

et fer

ho ent

ds f methods

or direc

for

ting dir

CA ecting

Vs traf CA

fic Vs

at j traf

un fic

ctio at

n junctions, 

s, 

it

it is crucial is

to cr

c ucial

ompa to

re compar

and eva e and

luate h evaluate

ow well how

ea

well

ch meth each

od a method

chieves itsachieves

object

its

ives i objectives

n 

in

order to 

or

spo der

t an to

y sh spot

ortcoany

min shortcomings

gs and he

and

lp the re help

searc the

her resear

s for th chers

e gap for

in t the

his gap

f

in

ield. this field. 

• 

At the •

end, At

the the

st end, 

udy d the

escr study

ibes thdescribes

e constra the

ints constraints

and offers and

sug off

gesti ers

on suggestions

s to help furt to

herhelp



further

study in thi study

s field.in

this field. 

According tAccor

o \[19\] ding

, the to

n \[

ex 19

t \], the

sectionnext

s of sections

the a

of

rticle a the

re a article

rran

ar

ged e

a arranged

s follows: as

Secfollows:

tion 2 of Section 2 of

the paper the

explapaper

ins th explains

e stra

the

tegies u strategies

sed to 

used

select th to

e prselect

ima

the

ry st primary

udies for studies

analysis for

ca analysis

refully; carefully; 

Section 3 prSection

esents 3

th pr

e fiesents

ndin the

gs an findings

d analys and

is of analysis

all the 

of

cho all

sen the

pri chosen

mary re primary

search; S resear

ection ch; 

4 

Section 4

presents, a pr

lonesents, 

g with along

some with

sug some

gestion suggestions

s for more for

re

mor

search e

, resear

the re ch, 

sult the

s co results

ncerni concerning

ng the ear- the earlier-

lier-posed posed

researc r

h esear

subj ch

ec subjects; 

ts; Section Section

5 pro 5

vid pr

es ovides

a sum a

m summary

ary of our of

finour

din findings. 

gs. Figure Figur

1 ex-e 1 explains

plains the the

pro pr

cessocess

and and

stag stages

es of th of

is this

st

study

udy. 

. 



**Figure 1. **Methodolo

**Figure **gy

**1. ** utilized in th

Methodologyis study. 

utilized in this study. 

**2. Research Me**

**2. thodolog**

**Research y **

**Methodology**

By the guidelines given in \[20\], this research conducted a thorough investigation and By the guidelines given in \[20\], this research conducted a thorough investigation and used the SLR to answer the research questions. It was attempted to complete the review’s used the SLR to answer the research questions. It was attempted to complete the review’s preparation, organizing, and reporting phases in several iterations to enable a thorough preparation, organizing, and reporting phases in several iterations to enable a thorough evaluation of the SLR. 

evaluation of the SLR. 

2.1. Primary Studies Selection

*2.1. Primary Studies Selection *

In this review paper, the study employed a simple search query to draw attention to the critical research in the relevant journals or search engines. Since the search was conducted in November 2022, it is safe to assume that it brought up any recent articles from 2022 or before that may be helpful for the RQs. The query string was limited to only run against the following paper titles, abstracts, and keywords to ensure the relevance of the chosen articles:



Appl. Sci. **2023**, 13, 1789

4 of 27

\(“AV” OR “autonomous vehicle” OR “self-driven” OR “driverless vehicle” \+ “interchange” OR “intersection” OR “roundabout” \+ “urban” OR “suburban” OR “rural” \+

“congestion” OR “capacity” OR “safety” OR “management” OR “detection”\)

As seen in Table 2, the inquiry encompassed five digital databases. The initial round of searches in the Digital Libraries turned up 315 items. The study found the remaining 140 papers using the inclusion/exclusion standards presented in Section 2.2 and a title, abstract, and keyword analysis to the search results. After comparing the whole texts of the remaining articles to the inclusion/exclusion criteria, 100 papers were found. The results were suitable for the run forward and backward snowballing, as outlined in \[21\]. Then, the study performed a reverse snowball by scanning all the reference lists in all the publications before doing a forward snowball, as shown in Figure 2. Then, the rest was examined, in which other publications correspond to the discovered set. 

*Appl. Sci. ***2023**, * 13*, x FOR PEER REVIEW 

5 of 28 



**Table 2. **Scientific database. 

**Online Scientific Database**

**URL Address**

Science Direct 2. When the inclusion/ https://www

exclusion cr .sciencedir

iteria 

ect.com/

were a

\(accessed

pplied to the o on 10

riginaNovember

l batch of 2022\)

articles, the 

IEEE Xplore Digital Library

number of papers was http://ieeexplor

reduced to 140. e.ieee.or

After g/

care \(accessed

fully exa on

m 11

ininNovember

g the rem 2022\)

aining reports 

Springer

https://link.springer.com/ \(accessed on 14 Novmber 2022\) considering the criteria, 87 major studies remained after the criteria were once again ap-Scopus

https://www.elsevier.com/solutions/scopus \(accessed on 18 Novmeber 2022\) plied. As described in \[22\], a backward and forward snowballing approach was then used Web of Science

https://www.webofscience.com/ \(accessed on 16 Novemeber 2022\) on the pertinent articles to find more primary papers to include in this SLR as 100. 



**Figure**

**Figure 2. **

**2. **Primary

Primary study

study filtering

filtering process. 

ocess. 

*2.4. *

2.2. * Quality Ass*

Inclusion

*es*

and *ment *

Exclusion Criteria

Using th

Findingse gu

that ide

ar li

e n

r es pr

equir ovi

ed d

to ed

be \[2

a 2\], th

part e 

of qua

this lity of prim

systematic a

r ry studie

eview

s 

must was a

show ssaessed to 

comput-

choose 

erized the 

apprreleva

oach n

tot publi

traffic cations to em

management ploy 

that and add

includes ress 

AVs the re

and searc

CVs, h questi

notably o

atns. In this 

junctions, 

roundabouts, and interchanges, and must provide analytical conclusions that take appli-study, five articles were selected at random and the quality evaluation procedure was cations and objectives into consideration. They must be available in the peer-reviewed used to determine the effectiveness of each one: 

*Traffic Management*: The study will discuss traffic control techniques while considering connected and autonomous vehicles. 

*Background*: To effectively respond to research question RQ1, the publication must give enough context for the study objectives and experimental findings. 

*Application:* The study must provide enough information to enable the recommended approach to be implemented in a specific traffic scenario to address research question RQ2. 

*Road user context*: The paper must consider passenger cars and avoid concentrating on public transit systems. 

*Performance evaluation*: To help with addressing question RQ3, the paper should include details regarding the assessment environment and solution models. The quality evaluation criteria then used primary studies located during the search process. Figure 3 

displays the total number of primary studies published by the different journals that make up our SLR between November 2012 and November 2022. 

Appl. Sci. **2023**, 13, 1789

5 of 27

journals listed in Section 2.1 and written in English. Articles that discussed law enforce-ment and speed management based on road restrictions were not included. The primary inclusion/exclusion criteria are listed in Table 3. 

**Table 3. **Inclusion/exclusion criteria. 

**Inclusion Criteria**

**Exclusion Criteria**

The manuscript presents analytical information

Papers that merely assess and contrast the

about the application and study goals. 

effectiveness of existing approaches. 

Papers focus solely on the management

Journal articles that have undergone peer

problem posed by purely human-driven

review. 

vehicles. 

Journal articles examining connected and

Technical reports or official government papers

autonomous automobiles. 

Non-English articles

2.3. Selection Results

In this study, a total of 315 research articles were obtained by preliminary keyword searches on the title, abstract, and keywords in the renowned libraries, as shown in Table 2. 

When the inclusion/exclusion criteria were applied to the original batch of articles, the number of papers was reduced to 140. After carefully examining the remaining reports considering the criteria, 87 major studies remained after the criteria were once again applied. 

As described in \[22\], a backward and forward snowballing approach was then used on the pertinent articles to find more primary papers to include in this SLR as 100. 

2.4. Quality Assesment

Using the guidelines provided \[22\], the quality of primary studies was assessed to choose the relevant publications to employ and address the research questions. In this study, five articles were selected at random and the quality evaluation procedure was used to determine the effectiveness of each one:

Traffic Management: The study will discuss traffic control techniques while considering connected and autonomous vehicles. 

Background: To effectively respond to research question RQ1, the publication must give enough context for the study objectives and experimental findings. 

Application: The study must provide enough information to enable the recommended approach to be implemented in a specific traffic scenario to address research question RQ2. 

Road user context: The paper must consider passenger cars and avoid concentrating on public transit systems. 

Performance evaluation: To help with addressing question RQ3, the paper should include details regarding the assessment environment and solution models. The quality evaluation criteria then used primary studies located during the search process. Figure 3 displays the total number of primary studies published by the different journals that make up our SLR

between November 2012 and November 2022. 

2.5. Data Extraction

In this study, the data were gathered from each study article validated during the assessment process to confirm the reliability and evaluate the information trail of chosen research. The study looked at the procedure for 140 first primary studies before applying the data extraction approach to all the selected research publications. Figure 2 depicts the method for choosing prior articles from a collection of publications discovered during the first searches. 





Appl. 

*Appl * Sci. 

*. Sci ***2023**

*. ***202 **, **3 **13

, * *, 

*13 * 1789

, x FOR PEER REVIEW 

6

6 of

of 27

28 



25

21

20

20

**ns**

**tioa**

**lic**

14

15

13

**ub**

**f P**

10

**or **10

7

**be**

5

**um**

4

5

**N**

3

2

1

0

2012

2013

2014

2015

2016

2017

2018

2019

2020

2021

2022

**Year \(2012–2022\)**



**Figure**

**Figure 3**

**3.. **Publications

Publications over

over time. 

time. 

*2.5*

2.6. *. Data *

Data *Extraction*

Analysis * *

In t

The his study, th

information e da

was ta were 

dividedgath

intoered from ea

qualitative ch 

and study article 

quantitative va

gr lidated

oups fr duri

om

ng

the the 

ana-

assessm

lyzed

ent pr

articles o

to ce

of ss 

fer to c

the onfirm 

study the reliabili

questions’

ty and

findings. ev

A aluate the 

systematic in

r forma

eview tion

was trail

also of chosen

performed 

re

onsearc

the h. 

scr The st

eened udy looked a

publications t the 

that pro

had cedure

been for 140

selected first pr

for

ima

further ry 

pr studies be

ocessing. fore applying 

the data extraction approach to all the selected research publications. Figure 2 depicts the 2.6.1. Publication Overtime

method for choosing prior articles from a collection of publications discovered during the first searc

Few hes. 

well-chosen studies were carried out between 2012 and 2016 despite the growth of AVs and CVs and their applications \(such as advanced driver assistance systems\) before *2.6. D*

2012. *ata Analy*

The

*sis *

number of primary studies that were selected is shown in Figure 3. As seen, traffic management is being used more frequently every year in transportation systems The information was divided into qualitative and quantitative groups from the ana-that include autonomous vehicles. 

lyzed articles to offer the study questions’ findings. A systematic review was also performed on the screened publications that had been selected for further processing. 

2.6.2. Substantial Keyword Distribution

The study used various traffic management techniques to look for the selected primary 2.6.1. Publication Overtime 

studies while considering phrases associated with self-driving vehicles. The frequency and Few well-chosen studies were carried out between 2012 and 2016 despite the growth suitable search phrases that are more commonly used for motorized and ground vehicle o

r f AVs 

esear

a

ch nd CVs an

techniques d th

are eir applica

stated in

tions 

Section \(such

2.1.  as advanced driver assistance systems\) be-

fore 2012. The number of primary studies that were selected is shown in Figure 3. As seen, tra

**3. **ffic man

**Research**agement is

**Analysis ** being used more frequently every year in transportation systems that in

Incl

r ude a

ecent utono

years, mo

theus ve

gr

hicles. 

owth of 

Information Technologies \(IT\), including robotics, signal

and image processing, computing, sensing, and communications, has coexisted with intelli-2.6.2

gent . Substantial K

transportationeyword Di

systems’ stributio

widespr n 

ead use. It is anticipated that current junctions will

The 

operate

stud

more y 

ef used va

fectively rio

byus traffic 

utilizing m

A a

V nagemen

and

t technique

communication s to look for 

technologies,the selec

such as ted

V pri-

ehicle-

mary 

to-V

stud

ehicle ies wh

\(V2V\), il

Ve con

ehiclesid

to ering ph

Infrastr rases 

ucture associa

\(V2I\), ted

and with se

Infrastr lf-drivin

uctur

g ve

e-to-V hicle

ehicle s. T

\(I2V he 

.s\) \[ fre

23 -

\]. 

quency

Using an

The d suita

Global ble search 

Positioningphrases 

System that are

\(GPS\), mo

laser, re com

Light monly u

Detectionsed 

andfor moto

Rangingrized and

\(LiDAR\), 

ground

camera, vehicle resea

ultrasonic

rch tec

sensors, hniq

and ues a

laser,re 

A sta

Vs ted in

may Secti

learn on 2

mor .e1. 

about their surroundings. As

a result, AVs are anticipated to improve the transportation system’s safety, effectiveness, **3. Re**

envir **search An**

onmental **alysis **

sustainability, and passenger comfort. 

This section examines alternative methods for controlling traffic made up of connected In recent years, the growth of Information Technologies \(IT\), including robotics, sig-and autonomous vehicles. Each main research article was carefully read and reviewed, and nal and image processing, computing, sensing, and communications, has coexisted with relevant qualitative and quantitative data were evaluated and reported in detail, as seen in intelligent transportation systems’ widespread use. It is anticipated that current junctions Table 3. Research Questions, as outlined in Table 1, were taken into consideration. 

will operate more effectively by utilizing AV and communication technologies, such as Vehicle-to-Vehicle \(V2V\), Vehicle to Infrastructure \(V2I\), and Infrastructure-to-Vehicle \(I2V.s\) \[23\]. Using The Global Positioning System \(GPS\), laser, Light Detection and Rang-



*Appl. Sci. ***2023**, * 13*, x FOR PEER REVIEW 

7 of 28 



ing \(LiDAR\), camera, ultrasonic sensors, and laser, AVs may learn more about their surroundings. As a result, AVs are anticipated to improve the transportation system’s safety, effectiveness, environmental sustainability, and passenger comfort. 

This section examines alternative methods for controlling traffic made up of connected and autonomous vehicles. Each main research article was carefully read and reviewed, and relevant qualitative and quantitative data were evaluated and reported in Appl. Sci. **2023**, 13, 1789

7 of 27

detail, as seen in Table 3. Research Questions, as outlined in Table 1, were taken into consideration. 

3.1. Driving Objectives

*3.1. Dr * Perspective

*iving Objectives Perspective *

The primary resear

The ch’

pr objectives

imary resea wer

rch’ e

o divided

bjectives into safety

were d

, ef

ividedfi

cacy

into , passenger

safety, eff

ease, 

icacy, passenger ease, 

ecology, and others based on the theme analysis. There is a piece concerning data-sharing ecology, and others based on the theme analysis. There is a piece concerning data-sharing features in the “other” class. To improve the accuracy of this study, significant goals include features in the “other” class. To improve the accuracy of this study, significant goals in-small subgoals. The outcomes are displayed in Figure 4. 

clude small subgoals. The outcomes are displayed in Figure 4. 



**Figure 4. **Main **Figure**

driving** 4. **Main dr

objectives ivin

andg objectives an

subobjectives. d subobjectives. 

3.2. Traffic Management Methodologies Consisiting of Primary Goals

*3.2. Traffic Management Methodologies Consisiting of Primary Goals *

The approaches for intelligent traffic management at high-conflict locations, such as The approaches for intelligent traffic management at high-conflict locations, such as junctions, roundabouts, and interchanges with AV and CV traffic, are the main emphasis junctions, roundabouts, and interchanges with AV and CV traffic, are the main emphasis of this section. Based on the RQ1 target list, the suggested techniques have been divided into categories as shown in Table 4. While some publications concentrated on a single goal, like efficiency, others considered many purposes, such as efficiency, safety, ecology, and passenger comfort. 

Appl. Sci. **2023**, 13, 1789

8 of 27

**Table 4. **Main findings of the major studies. 

**Driving Objectives**

**Adopted**

**Reference**

**Passenger**

**Methodology**

**Efficiency**

**Safety**

**Ecology**

**Comfort**

\[11,24\]

3

7

7

7

Hybrid

\[25\]

7

3

7

7

Hybrid

\[26–32\]

3

3

7

7

Hybrid

\[33\]

3

7

3

7

Hybrid

\[34,35\]

3

3

3

7

Hybrid

\[36\]

3

3

7

3

Hybrid

\[37–42\]

3

7

7

7

Machine Learning

\[43\]

7

3

7

7

Machine Learning

\[44–46\]

3

3

7

7

Machine Learning

\[47\]

3

3

3

3

Machine Learning

\[48\]

3

7

3

7

Machine Learning

\[49,50\]

3

3

7

3

Machine Learning

\[51–57\]

3

7

7

7

Optimization

\[58–61\]

7

3

7

7

Optimization

\[7, 62–69\]

3

3

7

7

Optimization

\[70\]

3

7

3

7

Optimization

\[33\]

7

3

3

3

Optimization

\[71–76\]

3

3

3

7

Optimization

\[36, 77\]

3

3

7

3

Optimization

\[47,50, 78,78–82\]

3

3

3

3

Optimization

\[83–90\]

3

7

7

7

Rule-Based

3.2.1. Efficiency

Numerous techniques have been used to enhance the efficiency of AVs and CVs in junctions, roundabouts, and interchanges. Different studies considered a variety of subgoals, including lowering traffic delays, increasing junction flow, and lowering the chance of congestion. The study examined the suggested strategies for improving conflict zones’ effectiveness. One paper \[91\] proposed a time-independent trajectory optimization strategy for connected and autonomous vehicles under reservation-based junction control to reduce the evacuation time of a group of vehicles. The method locates the best answer in terms of intersection efficiency. Similarly, the authors in \[51\] used a dynamic programming technique and the heuristic least extra time \(SET\). The effectiveness of the heritable, branch-and-bound algorithms, heuristic, and dynamic programming was compared by Yan et al. 

to that of the adaptive control and conventional stable-cycle-time systems. The findings demonstrated that the suggested approach could speed up evacuation times and shorten typical queues and vehicle wait times. Additionally, ref. \[52\] proposed a temporal delay Petri net-based \(TdPN\) control strategy to create a cooperative vehicle infrastructure system to enhance the intersection’s performance. The results show that when the traffic flow rate exceeds 1200 automobiles per hour, the TdPN approach beats conventional signal management systems associated with the delay, average queue length, average stop time, and average speed. 

Furthermore, ref. \[24\] provided an Autonomous Intersection Management technique based on an ant colony technique and discrete optimization technique to address real-time control issues with many vehicles and lanes considering an individual vehicle and real-time junction control. The suggested approach performs better than the current methods in terms of throughput, mean queue length, evacuation time, and mean vehicle delay. Similarly, ref. \[53\] suggested a game-theory-based approach for managing the Cooperative Adaptive Cruise Control \(CACC\) system-equipped autonomous vehicle movements at uncontrolled crossings. This research project aims to create an algorithm that can use connected and autonomous vehicles’ capabilities in the future to replace the conventional state-of-the-art control systems at junctions \(e.g., stop signs, traffic signals, etc.\). The suggested approach

Appl. Sci. **2023**, 13, 1789

9 of 27

is practical for use in real-time applications and was inspired by the chicken game. To provide their instantaneous speeds and positions, it is assumed that vehicles can interact with a central agent at the intersection. One paper \[83\] proposed PriorFIFO, a reservation-oriented priority scheduling approach, as a solution to the autonomous passing-through issue. Moreover, ref. \[84\] developed a unique reservation-based scheduling processor called csPrior-FIFO to prototype and build the traffic entities, such as service-oriented heterogeneous vehicles, centralized scheduler I-Agent, and their uniform behavior states. 

In terms of scheduling performance and latency, both approaches beat the FCFS technique. 

A time-sensitive programming approach was also suggested in \[85\] to address the RTD

issue. Under situations of high input flow, it outperforms AIM. 

Moreover, ref. \[86\] presented Batch-Light, an adaptive smart intersection control approach for AVs, which is a reservation-based control method. They employed a greedy-based conflict matrix decision algorithm to enhance the likelihood of a reservation with fairness. They also used a k-shift optimization approach to facilitate the junction passage of unlucky automobiles. The suggested technique surpasses FCFS and conventional traffic-light management strategies in conditions of average delay and the amount of traffic that successfully navigated the intersection in an hour while modeling balanced and unbalanced traffic. 

Additionally, ref. \[54\] suggested a junction system based on an auction that decides how many ideas there are for changing the sequence of the vehicles at the junction in all directions. It considers fostering justice while tolerating travel time for drivers on a restricted budget. Except for Baton Rouge, the recommended auction-based technique outperformed base cases on the road networks of four significant cities regarding trip time. 

Another study that uses automated vehicles to improve traffic flow on circular highways is \[87\], which used the cellular automation model to study the mixed traffic system at the micro level. Each AV in this system will have a “far-sightedness” and be capable of knowing the speeds and locations of the vehicles thanks to the use of sensors or mutual information exchange. They investigated how the extent of far-sightedness, the proportion of autonomous to human-driven vehicles, vehicle density, and the likelihood of random HV deceleration affect the traffic capacity in the circular road scenario. These formulae were shown to be essential for regulating the density and the proportion of HVs and AVs in future smart traffic systems, which will aid in preventing severe traffic congestion. 

Recent work \[88\] focused on the trajectory control of autonomous vehicles at traffic crossings using a newly developed non-linear tracking approach. The Newton–Raphson approach is used in this technique to direct an anticipated system output to a future reference goal. In considering the effectiveness of traffic flow at single-lane roundabouts, ref. \[8\]

proposed seven dispute resolution techniques. It prioritizes approaching vehicles using demand-dependent techniques and modifies their trajectories to consider the roundabout’s shape. The first technique arranges arriving vehicles based on their Shortest-Remaining-Time-First \(SRTF, i.e., the quickest period until the vehicle reaches the first dispute portion it will confront\) to the dispute segments within the circular roadway. In contrast, the other techniques adjust the SRTF regulations to satisfy highly unbalanced traffic flows with frequent right- or left-turning maneuvers. It was determined that the technology provides greater throughput with a more negligible average control latency than conventional vehicles’ operation. Under full CAV traffic flow, the roundabout’s capacity is enhanced by 58 to 73% \(with the increasing trend of conflicting flow, respectively\). In all demand situations, the approach that prioritizes vehicles that must pass through more dispute locations and those that exit the system first performs better than the other strategies, making it the best method for coordinating CAVs at roundabouts. According to procedures from the Highway Capacity Manual, this method minimizes the average control latency by 75 to 95% when compared to traffic with conventional vehicles. 

Reference \[55\] offers a cellular automata model based on many agents. The model can effectively simulate complicated traffic scenes using multi-agent theory to replicate complex traffic elements because cellular automata have simple rules and good simulation efficiency. 

Appl. Sci. **2023**, 13, 1789

10 of 27

The simulation’s outcomes demonstrate that the issue of swollen traffic volume-caused road congestion may be successfully prevented. A generalized macroscopic model was developed by \[56\] to predict the average connected autonomous vehicle \(CAV\) platoon length for a given traffic demand and CAV penetration rate. This model was used to analyze the capacity of roadways while taking mixed traffic into account to improve efficiency. The cooperative and opportunistic car-sharing strategies, representing the best- and worst-case outcomes, were contrasted. In addition, an investigation of the impact of autonomous driving vehicles on traffic jams in mixed traffic flows with both human and autonomous drivers operating randomly was performed. Another paper \[11\] compared three-traffic-phase ACC to traditional adaptive cruise control \(ACC\) \(TPACC\). It was demonstrated that ACC-vehicles may significantly worsen the traffic system while causing traffic breakdown and lowering highway capacity at a bottleneck throughout a wide range of dynamic parameters of classical ACC. Contrarily, the TPACC vehicles either have no impact on traffic characteristics in the same parameters as dynamic regulations of TPACC, or they can occasionally even make them better. 

In addition, ref. \[89\] outlined the general planning and decision-making methodologies for traffic management in recent years, including machine learning base, optimization base prediction-based, and graph-based approaches. Similar to this, ref. \[37\] defined the lane-changing decision-making of several AVs in a mixed-traffic highway environment as a multi-agent reinforcement learning \(MARL\) issue, where each AV bases its lane-changing judgments on the actions of both surrounding HDVs and AVs. According to thorough experimental research, their suggested MARL framework regularly beats several cutting-edge benchmarks in effectiveness, safety, and driver comfort. The authors of another study \[57\] employed a hierarchical design for cooperative intersection management to avoid network deadlock and reduce computational latency. They proposed the advanced cooperative vehicle-actuator system, with a deadlock-free protocol \(ACVAS\). It can reduce processing costs, recognize and resolve congestion, and reach conclusions quickly. Traffic management techniques aim to boost the infrastructure’s capacity to reduce traffic jams. 

In this context, ref. \[38\] offered a CAV-based alternative approach for traffic management, namely SWSCAV, and evaluated its effectiveness in comparison to other traffic management systems, such as lane control signals \(LCS\) and variable speed limits \(VSL\). In a simulation of the urban mobility \(SUMO\) environment, the recommended technique is assessed for 4800 scenarios on a three-lane highway by varying the market penetration rate of CAVs in traffic flow, the control distances, the incident lane, and the duration. The occurrence of densities surpassing 38 and 28 vehicles per km/lane at the event site is reduced by 12.68 and 8.15%, respectively, by the recommended technique. This study \[90\] provided a CV framework based on the Intelligent Vehicle Infrastructure Cooperative Environment that locates the vehicles using the two-way arrival time. To collect the vehicle kinematics data via the onboard system, the Kalman Filter \(KF\) is employed to increase the precision of the vehicle position. The associated method is then used to predict the trajectory of the vehicle. Data indicated that, compared to the results obtained before filtering, the suggested method’s vehicle speed and localization errors were reduced by 66.67% and 83.33%, respectively. It has been noted that research on autonomous vehicles is now moving away from conventional statistical models and toward adaptive machine-learning methods. As a result, ref. \[39\] offered a variety of deep learning techniques for increased AV efficiency. Similarly, ref. \[40\] sought to create a conceptual framework for addressing a list of requirements that considers several machine learning algorithms to identify the best algorithm for the intelligent regulation of AVs for a smooth flow through junctions. 

Furthermore, ref. \[41\] concentrated on the Variable Speed Limit \(VSL\) based on Q-Learning using CAVs as actuators in the control loop, considering mixed traffic in metropolitan regions. The observed findings demonstrate that Q-Learning based VSL can adapt to changing CAV penetration rates and learn the control policy while reducing travel times. 

In the same manner, ref. \[42\] studied and created a variable speed limit \(VSL\) based on Q-Learning \(QL\) using CAVs as operators and mobile sensors in combination with Speed

Appl. Sci. **2023**, 13, 1789

11 of 27

Transition Matrices \(STMs\) for prediction. it was found that the created algorithm was able to figure out the best strategy for each situation that was put to the test and enhance travel speeds. 

The rule-based techniques were categorized among those aiming for increased effectiveness \(e.g., \[55,57, 89\]\), then optimization \(e.g., \[56, 88,90\] hybrid \(e.g., \[11\]\) and machine learning \(e.g., \[39,40\]\). These various studies primarily focused on roundabouts and intersections. Most of the suggested techniques and base cases were examined in a simulated setting. 

3.2.2. Safety

One of AIM’s main objectives is to increase a specific intersection’s safety. By concentrating on several subgoals, such as preventing collisions and resolving potential conflicts, several strategies have been put forth to accomplish this aim. Model Predictive Control is a strategy presented by \[25\] to ensure the intersection’s traffic flow is free of collisions. For comparison, examples of simulations were created in the VISSIM and CarSim simulation platforms. Similarly, ref. \[58\] developed a cooperative driving technique for navigating intersections to reduce crashes and accidents. They suggested a decentralized method that enables moving vehicles to navigate intersections safely by successively resolving local optimization issues. Similarly, ref. \[92\] proposed a rule-based way to establish optimal vehicle order and safe braking while considering real-time collision detection. The speed control approach serves as the method’s foundation to prevent crashes, clarify the order of the vehicles, and let them pass through the uncontrolled junction. 

To reduce AV conflicts at an unsignalized junction, a cooperative approach was suggested in \[25\]; when a conflict was found, the proposed technique used the cost function to determine the best course of action for the vehicle. A centralized model predictive control \(MPC\) was also recommended by \[93\] to regulate the AVs crossing the junction and avoid crashes. They expressed the issue as a convex quadratic program in spatial coordinates to produce the best possible trajectories. They also considered penalized time gaps to boost safety in the event of sensor faults. Along the same line, to keep track of the control inputs and enhance vehicle safety \[92\], a mixed-integer quadratic programming \(MIQP\)-based real-time intersection supervisor was created to improve vehicle safety. The junction supervisor may override the vehicle control instructions to ensure safe operation. 

To address the coordination issue at intersections, ref. \[60\] proposed utilizing a dispersed and parallelizable technique called the augmented Lagrangian-based alternating direction inexact Newton \(ALADIN\) approach. 

Deep learning algorithms are also helpful for improving safety at intersections aside from that. One paper \[93\] suggested a safety framework based on the common Time to Collision \(TTC\) metric in this context. The framework primarily examines the possibility of lateral overlap and the time difference between the target vehicle and its surrounding vehicles. Later, an automated technique for developing trajectory data is constructed with image processing to generate the trajectory data from the study sections. With the growth of technology, it is now possible to produce trajectory data in real-time and put the safety framework in place. The essential areas of the road network may be identified using the research approach to receive better care and increase safety in such areas. 

In non-signalized junction scenarios, ref. \[60\] suggested a design strategy for the coordination of velocity profiles of autonomous vehicles. The synchronization is driven by the need to minimize energy loss caused by vehicle collisions and stop-and-go junction procedures. Another study \[94\] focused on connected autonomous vehicles working at smart crossings using a suitable navigation technique. This effort aims to develop a cooperative navigation system that will enable cooperative collision avoidance to improve the intersection’s capacity and safety. This research’s effectiveness is verified in a MATLAB/Simulink environment. Doing this prevents the car from hitting any other vehicles at the junction. 

As shown in Table 3, the techniques to enhance safety could be categorized as rule-based \(for instance, \[57, 94\]\), optimizing \(e.g., \[43, 61\]\), hybrid \(e.g., \[25\]\), and machine

Appl. Sci. **2023**, 13, 1789

12 of 27

learning \(e.g., \[43\]\) techniques to create conflict-free intersection management approaches. 

Highly suggested base cases and strategies were examined in a simulated setting. Most could ensure that no collisions occur at the junction \(for example, \[94\]; other techniques reduce conflicts \(e.g., \[26\]\). Even still, accidents could still happen during the flash hours. 

3.2.3. Safety and Efficiency

Enhancing the usefulness of suggested approaches in practical contexts requires finding the optimal balance between several aims. As a result, the articles in this section took both efficiency and safety into account. One study \[43\] suggested an ideal scheduling technique imagining the arrival time of AVs at the junction to reduce delays and increase safety. They used MILP to tackle the organizing issue, decreasing the frequency of stops and delays at crossings while preventing accidents. The suggested solution reduces average driving time and average halted wait by 7.6% and 52.5%, correspondingly, as contrasted with conventional traffic signal arrangements. Additionally, ref. \[95\] proposed a practical and safe technique called the customized synchronous intersection protocol \(CSIP\), a pow-erful and extensive variation of the ballroom intersection protocol \(BRIP\). CSIP employs a predefined inter-vehicle distance to get over this restriction and reduces the number of stops at the junction, since BRIP poses a danger of crashes due to positioning errors. As per the simulation findings, customized synchronous intersection protocol outperforms ballroom intersection protocol related to the number of trip delays and accidents. One study \[26\] addressed the issue of managing junction crossing traffic effectively and safely for connected and autonomous ground vehicles. They created a method known as a trajectory-based intersection traffic coordination algorithm for discrete-time occupations to achieve this goal \(DICA\). In the event of a communication breakdown, ref. \[96\] outlined a unique distributed intersection algorithm to prevent collisions and reduce delays at the junction. They discovered that the suggested approach successfully addresses numerous unidentified communication problems. Autonomous reservation-based intersection control \(AReBIC\), a novel approach \[97\], was proposed to reduce dispute and overall delay and to enhance mobility during an emergency evacuation. The recommended solution outperforms the current traffic control strategy in terms of average speed, overall delay, and conflicts and combines movement priority with a reservation methodology. To make intersections safer and reduce wait times, ref. \[27\] recommended a preassigned-slots approach employing the suitable optimization method for the initial allocation alternately transforming \(COMPACT\) and location improvement on sequence evaluation \(LOOSE\) for safety and higher effectiveness to enhance the performance of the target intersection. The suggested approach may shorten the average crossing time, and vehicles can pass through the junction without halting or colliding. 

For safe and quick intersection crossing, ref. \[63\] designed a smart multi-agent traffic controller. The suggested approach uses deep neural networks and reinforcement learning \(RL\) to learn and predict the optimum course of action for each vehicle. Additionally, considering V2I communication, ref. \[44\] introduced an intelligent in-vehicle decision-support system. It employed a probabilistic sequential decision-making procedure to assist AVs in making better stop/go decisions and minimizing needless stops. Another study \[28\]

created a decentralized coordination method based on sequential optimal control and model-based decision heuristics to tackle the traffic coordination problem. The suggested approach is collision-free and appropriate for quick online implementation. Additionally, ref. \[64\] described using 5G technologies to create communication-based apps for connected automobiles to increase efficiency and safety when using them. Similarly, ref. \[98\] described leveraging a 6G network for reliable and effective autonomous vehicle routing. 

Reference \[99\] suggested a delay-lenient protocol that considers transmission and network delay to increase junction management systems’ safety. The proposed approach surpasses conventional traffic signals in performance and average travel time conditions and prevents accidents. A hybrid centralized/distributed architecture was also created by \[65\] to coordinate AVs and enable vehicles to cross crossings safely and quickly. The

Appl. Sci. **2023**, 13, 1789

13 of 27

design employs a decentralized technique to prevent collisions and a centralized way to set the crossing duration with the maximum speed. The authors developed the reserve advance, act later \(RAAL\) and high-QoS-in-prior strategies \[29\] to accomplish these objectives. In the same spirit, authors modeled and constructed a standard cooperation mechanism for AVs to aid them in safely passing junctions. 

Another study \[30\] suggested a model to arrange the AVs at the junction based on the production line approach to prevent collisions and shorten wait times. They also used the K-Nearest Neighbors \(KNN\) method to anticipate how vehicles would proceed in a right turn. The simulation results show that the suggested model is more efficient for average and random traffic flow than the current paradigm. Reference \[100\] suggested a heuristic method to prevent space-time conflicts at the junction while considering the delay. Additionally, reference \[101\] developed an MPC-based central supervisory controller. 

The simulation results show that the recommended method beats the FCFS policy and traditional traffic lights in terms of transient reaction time and average delay. Another study \[102\] presented a distributed dispute resolution method using V2V communication to let CAVs traverse the signalized or unsignalized junction safely and effectively. Their study’s findings suggested that by reducing the average wait time, the proposed strategy would increase intersection efficiency. Reference \[103\] suggested an intersection coordination method based on mixed-integer programming to ensure safe and effective traffic flow in junctions \(MICA\). The proposed technique outperforms the optimal traffic-light mechanism and the trajectory-based intersection traffic coordination algorithm \[96\] in terms of traffic flow, according to the simulation results. 

By expanding the conventional single collision-set \(CS\) method, ref. \[66\] presented multiple-collision-set solutions to increase traffic throughput. According to the numerical findings, the suggested system might offer safe and effective traffic coordination. To manage the junction and coordinate vehicles, ref. \[104\] presented a collision-aware resource allocation \(CARA\) technique based on a self-triggered approach. Additionally, ref. \[67\]

suggested a dynamic coordinating framework based on the queuing theory to enhance the quality of service \(QoS\). The theoretical analysis and simulation results show that the recommended strategy can guarantee road stability and deliver high QoS. 

To increase junction efficiency and decrease traffic accidents, ref. \[105\] presented a game-in-game structure. The simulation results suggested that the framework may reduce accidents and boost productivity. Reference \[106\] put out a fresh approach using the evolutionary algorithm to improve intersection throughput automatically. To offer a realistic simulation environment, a cellular automata simulator was created. According to the simulation results, the suggested approach can increase throughput compared to the conventional method by 9.21–36.98%. A distributed management system to manage junctions was presented by \[68\] as a solution to the drawbacks of centralized traffic management systems. The simulation results demonstrated that the suggested solution performs better throughput than a traditional traffic control system. Similarly, ref. \[107\] proposed a method based on trajectory planning for autonomous intersection management \(TP-AIM\) to establish an accident trajectory and give priority and course to vehicles by assuming delay to increase the safety and efficiency of an unsignalized intersection. As a result, the throughput increases by more than 20%, while the average evacuation time is minimized. 

Additionally, the junction delay is decreased to less than 10% compared to the standard traffic signal. Reference \[108\] suggested using decentralized coordination learning of autonomous intersection management \(DCL-AIM\) to optimize control strategy to reduce delays and prevent collisions at the intersection. Multi-agent Markov decision processes \(MAMDPs\) represent vehicles’ sequential movement, and reinforcement learning, particularly multi-agent reinforcement learning, is used to address the problem. According to the simulation findings, the DCL-AIM performs better than the current control techniques. 

A distributed cooperative control has been developed to avoid collisions between connected and autonomous vehicles at an unsignalized crossroads \[31\]. A distributed synchronized signal-free intersection control logic is known as \(DC-SICL\). According to the

Appl. Sci. **2023**, 13, 1789

14 of 27

simulation’s findings, the suggested technique outperforms an optimum actuation signal control in terms of travel time, traffic flow, and safety. Another study \[45\] suggested a dispute-avoidance-based strategy for managing vehicles at the unsignalized crossroads by considering all-direction turn lanes \(ADTL\). The simulation results showed that, with assured collision avoidance, the suggested technique outperforms conventional traffic signals in terms of throughput and trip time. In addition, they offered a development approach to increase throughput at an unsignalized junction without increasing the danger of an accident. They created the individual and car sharing-based arrival model, which uses the optimal entry time scheduling \(OETS\) method and a heuristic algorithm. Compared to conventional traffic signals, the suggested strategy reduces traffic delays and increases efficiency \[109\]. 

A visible light communication \(VLC\)-based collision avoidance strategy is presented to coordinate autonomous vehicles in crossing roundabouts, which has excellent efficacy in vehicular contexts to prevent traffic jams or major accidents \[69\]. At the roundabout entrances, roadside units \(RSUs\) are set up to coordinate the vehicles in a vehicle-to-infrastructure \(V2I\) mode. Vehicles can pass the roundabout concurrently using the synchronization strategy if their trajectories are parallel. Otherwise, traffic is prioritized based on arrival time, and proper braking is used to avoid potential problems. Simulation findings show that our suggested technique fulfills the roundabout traffic demands in concurrency, safety, and time utilization, since only 22% of the situations investigated in the various scenarios strongly advise vehicles to slow down. Similarly, ref. \[32\] developed and tested a variety of spatiotemporal-based algorithms for autonomous, connected vehicles to enable safe and effective junction crossing. Vehicles communicate using dedicated short-range communications \(DSRC\) through vehicle-to-vehicle \(V2V\) communication. To improve safety and efficiency when interacting with other traffic participants, ref. \[110\] developed a multi-task safe reinforcement learning framework with social attention. In recent years, autonomous vehicles have been challenging to navigate in intersections and between heavy traffic. They set up trials in the simulators CARLA, which has very realistic vehicle models, and SUMO, which has a lot of traffic. Both examples demonstrated how the suggested approach for the multi-task junction navigation problem increases safety while maintaining steady traffic efficiency. Additionally, ref. \[111\] offered an intelligent overtaking choice for an autonomous vehicle based on the heuristic reinforcement learning approach. The proposed overtaking control is centered on the effectiveness and safety of operating an autonomous vehicle. 

As shown in Table 3, different strategies have been devised to increase intersection productivity while considering safety. Four optimization techniques, according to researchers, can be used in real-time or online applications \(\[62, 104,107,108\]\). Most of the suggested techniques and base cases were examined in a simulated setting. The anticipated approaches outperformed base cases with 10–450% boosts and 0–26% declines when considering various performance metrics. Most tests employed a single intersection with simplified traffic circumstances to validate the suggested methodologies. 

3.2.4. Efficiency and Ecology

Specific papers suggested several techniques to manage AV traffic at conflicting zones while considering efficiency and ecology. One study \[46\] suggested a method they called

“cooperation between a traffic signal and vehicles \(CTV\)”, which determines the best signal timing, driving order, and arrival time for each vehicle. AVs’ trajectory, engine power profile, and acceleration/deceleration behavior are optimized when utilizing optimal control. When compared to the actuated signal control approach, the recommended strategy reduces average travel delays and average fuel economy by 19.8% and 23.8%, respectively. Initial vehicle clustering, intra-cluster sequence optimization, and cluster formation management are all components of the cluster-wise cooperative eco-approach and departure application \(coop-EAD\), developed by \[70\] to reduce energy use, emissions, and traffic throughput. The suggested coop-EAD approach outperforms the current ego-

Appl. Sci. **2023**, 13, 1789

15 of 27

EAD method in terms of energy usage and traffic flow by 11.0% and 50%, respectively. 

Moreover, 2.29–19.91% less pollution is emitted as a result. 

Recently, considering mixed traffic flows, ref. \[48\] focused on the issue of minimizing traffic’s harmful environmental effects, such as congestion, energy and gasoline utilization, and flue gas pollution. They used electric CAVs as speed-limit operators in the control loop of a variable speed limit \(VSL\) based on Q-Learning. The collected findings demonstrate that Q-Learning-based VSL can train the control strategy for various electric CAV

penetration rates, improve the macro traffic parameters and total energy consumption, and minimize exhaust gas emissions. 

Table 3 displays several strategies; altogether, the suggested solutions exceed the virtual instances by 2.30–60% when various performance measures are considered. Additionally, to validate the proposed methodologies. 

3.2.5. Ecology, Passenger Comfort, and Safety

One article on traffic management \[48\] discussed three objectives—ecology, passenger comfort, and safety—and proposed a decentralized optimum control system to reduce fuel consumption and passenger discomfort while maintaining safety. The study’s findings \[33\]

suggested that the suggested strategy is appropriate for online deployment. 

3.2.6. Efficiency, Safety, and Ecology

The papers that jointly addressed efficiency, safety, and ecology are included in this section. At an unsignalized junction, ref. \[71\] suggested the vehicle-intersection coordination system \(VICS\), based on the MPC architecture, which aims to reduce fuel consumption and increase traffic efficiency. Compared to a traditional signalized intersection, the proposed technique improved intersection performance variables, such as vehicle stop times, traffic flows, fuel consumption, and intersection capacity. Additionally, by splitting the junction into three primary communication zones, ref. \[112\] presented a novel intersection model based on the multi-agent reservation technique to reduce overall delays and power loss and increase accident detection. This tactic decreased both the overall delay time and power loss. Additionally, it reduces energy waste, prevents crashes, and efficiently traverses intersections. A multi-objective evolutionary algorithm \(MOEA\) was also suggested by \[113\]

to find safe routes for AVs in a junction by safely and efficiently routing vehicles. The simulation results show that the strategy works well in low-traffic situations. To obtain nearly optimum CAV paths free of junction conflicts, ref. \[114\] suggested signal-head-free intersection control logic \(SICL\). The proposed approach employs stochastic lookahead to minimize intersection throughput, reduce travel time, eliminate pauses, and minimize fuel consumption. Comparing the proposed method to signal control approaches, travel time may be cut by 59.4–83.7% depending on the kind of traffic. To reduce travel time, energy use, and fuel consumption while maximizing throughput at an unsignalized junction with guaranteed safety, ref. \[34\] suggested a decentralized energy-optimal control system. Comparing the recommended method to the current traffic signal management systems, it is possible to achieve fuel savings of 47% and travel time reductions of 31%. 

Platoon-based autonomous intersection management \(PAIM\), proposed by \[72\] to reduce interruption and inconsistency at the junction, is a centralized platoon-based controller based on reservation policy and cost function. The suggested strategy works better than traffic signals regarding delay and fuel usage. To reduce accidents and enhance traffic at the junction, ref. \[73\] proposed a decentralized approach called the cooperative intersection control \(CIC\) technique. The simulation results show that the suggested technique performs better throughput and latency than the conventional traffic light. 

A novel junction management method considering the non-linear vehicle dynamic model and meteorological circumstances was suggested by \[115\]. By up to 80.0%, 40.0%, and 42.5%, respectively, the proposed technique decreased delay, CO2 emission, and fuel use based on the simulation’s findings. To find the best answers, the proposed approach may have a high computing cost. Research \[116\] proposed a strategy based on cooperation

Appl. Sci. **2023**, 13, 1789

16 of 27

between AVs and the roadside unit to increase junction effectiveness and reduce fuel usage. 

The suggested approach performs better than both traditional fixed switching and cutting-edge algorithms. Another study \[35\] presented a cooperative approach to regulate the speed of AVs at the intersection and optimize traffic signals. According to the simulation findings, when traffic demand is between 800 and 3200 vehicles per hour, the suggested solution results in less fuel usage and travel time than actuated signal control. Codrive, a cooperative speed advisory system, was suggested by \[74\] to reduce fuel usage at signalized junctions. According to the simulation results, the fuel consumption is lower compared to the Green Drive by 7.9 to 38.2%. 

Additionally, ref. \[75\] suggested an approach for increased safety, decreased fuel use, and less transportation congestion and pollution. They investigated the effects of achieving a smooth traffic flow on roundabouts by wirelessly connecting vehicles and coordinating them as efficiently as possible. Through simulation, the effectiveness of the suggested strategy is confirmed, and it is demonstrated that completely coordinated vehicles cut the overall trip time by 51% and fuel consumption by 35%. Various techniques have been devised to increase intersection effectiveness, lessen the environmental impact, and preserve traffic safety, as indicated in Table 3. Considering multiple performance measures, the suggested approaches beat the base instances by 2.8–95%. Again, most of the research validated the proposed solutions using a single crossing with skewed traffic circumstances. 

3.2.7. Efficiency, Safety, and Passenger Comfort

In this section, the papers that concurrently evaluated efficiency, safety, and passenger comfort because these factors are crucial for controlling traffic were examined. 

Reference \[117\] offered an uncoupled and dispersed solution that employs graph-based algorithms to optimize longitudinal trajectories for many vehicles at metropolitan crossings while considering efficiency, passenger comfort, and accident avoidance. Compared to the intersection control approach for human-driven autos and a non-cooperative control strategy, the recommended method can improve junction performance. Reference \[76\]

created an automated intersection control \(AIC\) to enhance system fairness, safety, throughput, travel time, and passenger experience. To schedule vehicles and ensure that they cross the junction quickly and smoothly, the quality-of-experience-oriented autonomous intersection control \(QEOIC\) method was recommended by the authors. By predefining the decision zone and dividing the junction into numerous collision zones, they also developed a scheduling algorithm to determine the priority of the automobiles in different collision regions, which linearized the collision constraints. They emphasized that the suggested method may be used to implement real-time traffic control. 

Similarly, ref. \[77\] suggested a self-organizing and collaborative framework to direct vehicles over a junction without confrontation. The proposed technique performed better than the conventionally actuated process in terms of overall latency. To prevent accidents and traffic jams, increase safety, and enhance passenger comfort, ref. \[36\] presented Dynamic Traffic Congestion Management in Social Internet of Vehicles \(SIoV\). In their article, they suggested a traffic scheduling algorithm to maximize throughput for the movement of vehicles at a road intersection while including social ties between the moving vehicles and the roadside units \(RSUs\). The algorithm uses the amount of traffic on the given route to predict the flow rate of vehicles for lanes at junctions. A condition matrix is created to ensure smooth traffic flow while considering various road segment routes. Social interactions are developed on various travel-related demands to make driving more secure, responsive, and enjoyable. The simulation findings show how the suggested plan is more effective than the Dynamic Throughput Maximization Framework and Adaptive Traffic Control Algorithm in terms of high traffic throughput, service rate, and a reduction in total journey time, delay time, and average waiting time. 

The Elman neural network \(ENN\) model was created by \[118\] and optimized with the sparrow search algorithm \(SSA\) to establish a connection between connected autonomous vehicles and human-driven automobiles \(CAVs\). The numerical simulations demonstrate

Appl. Sci. **2023**, 13, 1789

17 of 27

that the driving approach can increase road capacity and reduce traffic oscillations. Traffic effectiveness, safety, and driving comfort enhance as CAV penetration rises. Recently, in 2022, using the same approach, ref. \[49\] examined communication quality prediction in mobile Internet of Vehicles \(IoV\) networks. New Outage Probability \(OP\) terms that may evaluate the performance of model were developed. Then, an intelligent OP prediction strategy using an Elman model was suggested for real-time OP prediction. This was assessed using information produced by the OP terms. The findings collected suggest that the Elman-based strategy delivers superior forecasting effect than other approaches in terms of computing difficulty and accuracy rate. 

Considering Machine Learning techniques in recent years, ref. \[50\] provided a thorough overview of Variable Speed Limit \(VSL\) and Ramp Metering \(RM\) control algorithms, encompassing the most modern methods based on reinforcement learning. 

Optimization techniques, including rule-based and hybrid approaches, have been established to increase crossroads’ effectiveness and environmental impact while considering traffic safety and passenger comfort, as shown in Table 3. Overall, the throughput and overall latency of the suggested approaches are better than the primary instances. 

Additionally, most tests employed a single intersection with simplified traffic circumstances to validate the proposed methodologies. 

3.2.8. Efficiency, Safety, Ecology, and Passenger Comfort

Future traffic management methods may be most effective if they can simultaneously consider all four categories of goals and strike a reasonable balance between them. 

Ding et al. \[36\] suggested a non-linearly constrained programming problem formulation for a centralized cooperative intersection control strategy for unsignalized junctions. The recommended technique may decrease travel time by 88.56–95.38%, increase fuel efficiency by 17.18–37.81%, and enhance traffic flow by 10.49–17.61% compared to actuated junction control. Furthermore, it lowers CO2 emissions by 61.13 to 67.6%. Reference \[49\] detailed the advantages of six alternative real-time traffic management techniques, including traffic diversion, ramp metering, changing message signs, dynamic speed restrictions, and lane control systems. These plans are assessed using 13 subcriteria prioritized using fuzzy multi-criteria decision-making and the four core criteria of economic, public, political, environmental, and traffic safety \(MCDM\). For this purpose, the combined compromise solution \(CoCoSo\) approach was presented with the distinctive additions of the logarithmic technique and the Power Heronian function. 

A semi-decentralized multi-agent-based vehicle routing system, considering trip time prediction and computing efficiency, was developed in \[49\] to enhance the likelihood of arriving on time, travel time, driver satisfaction, accident rate, fuel usage, and emissions. 

The experimental results of \[50, 78–80\] showed that it outperforms existing methods in terms of factors such as average total journey time, fuel consumption, and air pollution. For unsignalized intersections, ref. \[47\] developed a method for multi-objective optimization to coordinate the CAVs to lower fuel consumption, boost traffic efficiency, and improve driving comfort. The recommended solution, which requires low computational work and ensures safety, increases CAV effectiveness, fuel efficiency, and ride ease, according to the simulation results. 

Reference \[81\] suggested a novel method to steer CAVs across a junction utilizing traffic-light information and infrastructure-to-vehicle communication to save travel time and fuel consumption. According to the simulation, the suggested algorithm surpasses human-driven vehicles in terms of energy usage and trip time. Optimization, rule-based, and machine-learning techniques have been established to increase intersection effectiveness and environmental impact while considering traffic safety and passenger comfort, as shown in Table 3. Overall, the suggested approaches’ throughput, fuel use, and trip time are better than the basic scenarios. Most of the tests employed a single intersection with simplified traffic circumstances to validate the suggested methodologies. 





*Appl. Sci. ***2023**, * 13*, x FOR PEER REVIEW 

18 of 28 



driving comfort. The recommended solution, which requires low computational work and ensures safety, increases CAV effectiveness, fuel efficiency, and ride ease, according to the simulation results. 

Reference \[81\] suggested a novel method to steer CAVs across a junction utilizing traffic-light information and infrastructure-to-vehicle communication to save travel time and fuel consumption. According to the simulation, the suggested algorithm surpasses human-driven vehicles in terms of energy usage and trip time. Optimization, rule-based, and machine-learning techniques have been established to increase intersection effectiveness and environmental impact while considering traffic safety and passenger comfort, as shown in Table 3. Overall, the suggested approaches’ throughput, fuel use, and trip time Appl. Sci. **2023**, 13, 1789

18 of 27

are better than the basic scenarios. Most of the tests employed a single intersection with simplified traffic circumstances to validate the suggested methodologies. 

3.2.9. 

3.2.9. Other:

Other: Data

Data Sharing

Sharing 

To

To reduce

reduce AIM’s

AIM’s complexity

complexity and

and data

data exchange, 

exchange, a an

n exexpanded

panded ve version

rsion of of

A AIM

IM is dis

e-

described

scribed in in

\[82\[\]82

. \]. The

The authauthors

ors crea created

ted the the

incr incr

emen emental

tal data data

synchrsynchr

onizationization

on stra

strategy

tegy known 

known

as ksy as

nc fksync

or d

for

river driver

agents agents

to min to

immi

iz nimize

e data data

tran

transfer

sfer and and

prev pr

ent event

redu r

n edundancy

dancy from from

max-

maximizing

imizing ban bandwidth

dwidth utili utilization. 

zation. Acc Accor

ordin ding

g to to

ex

experimental

perimental ass assessments, 

essments, the the

ave average

rage data 

data

com compr

pressi ession

on rate rate

can can

incr incr

ea

ease

se 

by

by mo mor

re th e

anthan

75% 75%. 

. 

**4. **

**4. Discussion**

**Discussion **

To r

To espond

respon to

d all

to a the

ll th resear

e re

ch

searcquestions

h questio in

ns Table

in Ta 1 for

ble 1 this

for systematic

this system literatur

atic liter e

a review

ture re ,-

the analytical

view, the ana arrangements

lytical arrangemof the

ents of significant

the sign

studies

ificant stud are

ies pr

areesented

presen in

ted this

in th part. 

is part. The





study

study also

also of

o fers

ffer specific

s spec

analytical

ific analytica charts

l charts following

following the

the technical

technical questions

questions to pr

p ovide

rovide a 

comprehensive overview of the examined material. A summary of the pertinent qualitative comprehensive overview of the examined material. A summary of the pertinent qualita-and quantitative data is included in Table 3. 

tive and quantitative data is included in Table 3. 

RQ1: What driving objectives did traffic management studies consider while us-RQ1: What driving objectives did traffic management studies consider while using ing AVs? 

AVs? 

Figure 4 displays the primary driving goals that have received the greatest attention Figure 4 displays the primary driving goals that have received the greatest attention when using AVs and CVs. The combination of effectiveness, safety, ecology, and passenger when using AVs and CVs. The combination of effectiveness, safety, ecology, and passen-comfort was the most crucial problem researchers have tackled, as shown in Figure 5. 

ger comfort was the most crucial problem researchers have tackled, as shown in Figure 5. 

****

Others

1

**byd es **Efficiency/Safety/Ecology/Passenger Comfort

8

**sre**

Safety/Ecology/Passenger Comfort

1

**dda se rs**

Efficiency/Safety/Passenger Comfort

7

**tiv**

**he**

**c**

**rca**

Efficiency/Safety/Ecology

12

**bje**

**es**

**O**

**e**

****

**R**

Efficiency/Ecology

3

**ingiv**

Efficiency/Safety

34

**Dr**

Safety

10

**in **

**Ma**

Efficiency

24

0

5

10

15

20

25

30

35

40

**No. of Articles**



**Figure 5. **Categorization of different driving objectives in the major studies. 

**Figure 5. **Categorization of different driving objectives in the major studies. 

RQ2: What traffic management techniques have been suggested to handle the possible issues brought on by AVs? 

Figures 6 and 7 provide an overview of the methods put into practice to address the traffic management problems at junctions, interchanges, and roundabouts. As seen in this picture, the examined literature has mainly used optimization approaches and rule-based procedures to handle this challenge. 





*Appl. Sci. ***2023**, * 13*, x FOR PEER REVIEW 

19 of 28 



RQ2: What traffic management techniques have been suggested to handle the possible issues brought on by AVs? 

Figures 6 and 7 provide an overview of the methods put into practice to address the traffic management problems at junctions, interchanges, and roundabouts. As seen in this *Appl. Sci. ***2023**, * 13*, x FOR PEER REVIEW 

picture, the examined literature has mainly used optimization approaches and rule 19

- o

ba f 28

sed 



procedures to handle this challenge. 

RQ2: What traffic management techniques have been suggested to handle the possi-Distribution of Articles based on methodologies

ble issues brought on by AVs? 

Figures 6 and 7 provide an overview of the methods put into practice to address the traffic management problems at junctions, interchanges, and roundabouts. As seen in this Appl. Sci. **2023**, 13, 1789

19 of 27

picture, the examined literature has mainly used optimization

Opt iappr

mi o

zat a

i ches 

on

and rule-based 

procedures to handle this

**14%** challenge. 

**39%**

**13%**

Rule Based

**Distribution of Articles based on methodologies**

Hybrid

**34%**

Machine Learning

Optimization

**14%**

**39%**



**13%**

Rule Based

**Figure 6. **Article distribution depending on the methodology. 

Hybrid

RQ3: What concerns and issues in traffic management techniques still need to be re-34%

solved? 

Machine Learning

To respond to RQ3, the remaining flaws and gaps in the original research were examined while considering the methodology and validation environment. 

From a methodological standpoint, the available approaches were grouped into four main groups based on the outcomes investigated under RQ2: rule-based, machine learn-Figure 6. Article distribution depending on the methodology. 

**Figure 6. **Article distribution depending on the methodology. 

ing, hybrid, and optimization-based learning. 

RQ3: What concerns and issues in traffic management techniques still need to be re-16

solved? 

14

14

To respond to RQ3, the remaining flaws and gaps in the original research were examined while considering the methodology and validation environment. 

**s **12

10

**le**

From a

10 methodological standpoint, the available approaches were grouped into four 10

**ticr**

main groups based on the outcomes investigated under RQ2: rule-based, machine learn-7

7

7

**A **8

**f**

6

6

ing, hybrid, and optimization-based learning. 

**o**

5

6

**o. **

4

**N**

3

3

4

16

2

2 2

2

14

1 1

1

1 1

1

1

1

1

1

2

14

0

0

0 0 0

0 0

0

0 0

0

**s **12

10

10

**le **10

**ticr**

7

7

7

**A **8

**f**

6

6

**o**

5

6

**o. **

4

**N**

3

3

4

2

2 2

2

1 1

1

1 1

1

1

1

1

1

2

0

0

0 0 0

0 0

0

0 0

0

**Main Driving Objectives addressed by Researchers**

Optimization

Rule Based

Hybrid

Machine Learning



**Figure 7. **Article distribution depending on techniques and driving objectives. 

RQ3: What concerns and issues in traffic management techniques still need to be resolved? **Main Driving Objectives addressed by Researchers**

To respond to RQ3, the remaining flaws and gaps in the original research were exam-Opt

ined imiza

whiletion

Rule

considering Base

the d

Hybrid

methodology andMachine Lea

validation rning

environment. 

From a methodological standpoint, the available approaches were grouped 

into four

main groups based on the outcomes investigated under RQ2: rule-based, machine learning, hybrid, and optimization-based learning. 

Firstly, most of the rule-based techniques now in use \(such as \[24, 37,52,53\]\) were created to increase junction efficiency and/or safety for AV-only or mixed-traffic situations. 

Rule-based approaches can be used for real-time junction management techniques and vehicle control due to their computational simplicity \(e.g., \[42\]\). Additionally, rule-based

Appl. Sci. **2023**, 13, 1789

20 of 27

methods are utilized to develop comprehensible and understandable models. A few rule-based methods have been verified by field testing or actual data \(e.g., \[42\]\). However, the model’s goals and restrictions greatly enhance the complexity of the rule-based approach. 

Therefore, when more plans are considered in the rule-based strategy, the amount of enhancement of the target factors reduces. Because the rule-based technique uses statistical criteria and cannot ensure the outcomes are ideal, it has the additional disadvantage that performance may vary depending on traffic circumstances. 

Secondly, approaches based on optimization have been established to deal with single-goal or several-goal situations \(e.g., \[38, 86, 115\]\). Many optimization forms or searching algorithms have been devised or used to increase computing efficiency and discover optimal solutions. By adjusting objective functions, restrictions, and searching algorithms, the optimization-based approach can easily handle many goals and complicated situations. Methods based on optimization always look for the best answers for various traffic situations. 

Therefore, when optimality is ensured, optimization-based solutions provide optimum performance under different traffic situations. However, the time frame needed for intersection management may not always be satisfied by optimization-based approaches in terms of global optimum solutions. Additionally, when traffic volume and situation complexity increase, optimization-based approaches’ computational complexity also considerably increases \(e.g., \[36\]\). As a result, only a handful of the currently used optimization-based methods were thought to be suitable for real-time control \(e.g., \[76, 92,101\]\). Based on the outcomes of simulations, the current optimization-based methodologies have been validated. 

Thirdly, only a small number of studies \(such as \[90\]\) used hybrid techniques to address issues with intelligent intersection control connected to efficiency and safety. Rule-based and optimization-based techniques are combined in hybrid approaches. Hybrid approaches take less time to compute than optimization-based methods, since they are somewhat based on rules, which reduces their computational complexity. In contrast to rule-based systems, the optimization component of hybrid methods enhances their adaptivity. However, a distinct blend of rule-based and optimization-based techniques can provide noticeably different results. It is not easy to integrate the rule-based strategy and the optimization-based method. Balancing numerous aims and assuring performance is another frequent issue with the current approaches. Additionally, considering the techniques’ validation environment highlighted shortcomings and inadequacies. First, the validation process’s consideration of traffic circumstances was overly simplistic compared to actual traffic patterns at crossings. A few suggested approaches were only evaluated in predetermined traffic scenarios with set traffic flow rates. The volume of traffic, however, fluctuates according to the time of day, the day of the week, the weather, and other factors. 

For instance, the methods described in \[77\] are more efficient and effective when there is little traffic than when there is significant traffic. Several techniques, such as \[59\], were validated by considering various traffic scenarios and circumstances. In some publications, balanced traffic at the crossroads, interchanges, and roundabouts was considered, but the types and quantities of traffic coming from various directions tend to change. Next, the majority of the car details and driving styles were improbable. Deterministic vehicle features have been employed in previous investigations \(for instance, \[84\]\) and car-following behavior parameters, While the driver-behavior parameters for human-driven automobiles in real-world traffic \(such as duration, headway, standstill distance, and so on\) are stochastic. Additionally, different automakers outfit their creations with sensors of varying caliber, and they have access to a variety of algorithms for automatic movement. Furthermore, the controllers for various vehicle types with variances in size and weight \(such as trucks, passenger cars, vans, and so on\) may change. 

Fourthly, many techniques have been verified in simulation settings \(for instance, \[27\]\). 

Platforms for simulation might be unable to correctly represent real-world circumstances, including geometry restrictions, weather, and pedestrian movement. It continues to be challenging to create approaches for taking V2X communication technology restrictions into account in simulations. 

Appl. Sci. **2023**, 13, 1789

21 of 27

**5. Conclusions**

Autonomous and connected vehicles have long been studied topics in the framework of ITS. This study examined current studies on traffic management strategies that use AVs and CVs to improve road safety and promote safe travel. Additionally, summarizing these strategies and analyzing the results and goals attained are interesting. This study acquired an extensive understanding of the various traffic management strategies used, the open problems in this area, associated difficulties, and future directions. 

•

A comprehensive review of 315 publications that were published between 2012 and 2022 was given in this study. In the end, this research examined 100 studies on traffic management, including AVs and CVs at junctions, interchanges, and roundabouts that had passed the quality evaluation. According to statistics on the number of research papers published on this subject each year from 2018 to 2022, additional research is anticipated in 2023–2024, particularly in machine learning techniques. 

•

The primary goal of this literature review was to describe the most recent publications in the field of connected and autonomous vehicles to understand current traffic management techniques and identify difficulties and limitations. The study addressed three research questions, as per the analytical discussions. The approach recommended by \[107\] generated the maximum performance for the techniques described in this research out of all the articles considered in this evaluation. However, Due to the inability of human-driven cars to rationally communicate and cooperate with other road users, mixed traffic at unsignalized intersections may be difficult to evaluate in such a technique. Rule-based approaches made up 34% of the papers chosen, followed by optimization techniques at 39%, hybrid methodologies at 13%, and 14% of the publications that were chosen employed ML techniques. 

•

The study assessed the behavior of the recommended approaches associated with effectiveness, safety, environmental effects, and passenger ease, and the study’s findings were published. Investigators utilized numerical testing, math, simulators, mathemat-ics, numerical testing, and other techniques in 95% of the selected articles to support their theories, whereas 5% used toy vehicles, actual automobiles, or field tests. It is recommended that AI-based traffic management structures may minimize some of the issues said by optimizing the data collection method. This may include learning traffic characteristics and human behaviors, projecting traffic attributes, and creating more effective traffic-management decisions. The recommended approaches should be more extensively assessed to cope with sensor variation, since car manufacturers install various sensor types with varying features and quality to collect data. 

•

Finally, RQ3 was addressed by discussing the primary research’s remaining shortcomings and gaps while considering various factors, such as methodology and validation environment. In total, 90% of research has focused on pure AVs, in contrast to the reality, which will soon involve a combination of human-driven automobiles, AVs, pedestrians, and bicycles. 

As a result, one potential study area is leveraging AV characteristics to gather environmental data in mixed traffic to enhance traffic management system performance. It continues to be challenging to create approaches for taking V2X communication technology restrictions into account in simulations. Nevertheless, a further survey concentrating on traffic management can be performed, given the rising quantity of research articles in this area. 

**Funding: **This research received no external funding. 

**Institutional Review Board Statement: **Not applicable. 

**Informed Consent Statement: **Not applicable. 

**Data Availability Statement: **Not applicable. 

**Conflicts of Interest: **The authors declare no conflict of interest. 

Appl. Sci. **2023**, 13, 1789

22 of 27

**Abbreviations**

The following abbreviations are used in this review paper. 

ITS

Intelligent Transportation System

AV

Autonomous Vehicles

CV

Connected Vehicles

HV

Hybrid Vehicle

CAV

Connected And Autonomous Vehicles

SAE

Society Of Automotive Engineers

ACC

Adoptive Cruise Control

TPACC

Three-Traffic-Phase Adaptive Cruise Control

CACC

Cooperative Adaptive Cruise Control

SLR

Systematic Literature Review

IEEE

Institute Of Electrical and Electronics Engineers

IT

Information Technologies

V2V

Vehicle-To-Vehicle

V2I

Vehicle To Infrastructure

I2V

Infrastructure-To-Vehicle

GPS

Global Positioning System

LiDAR

Light Detection and Ranging

TdPN

Temporal Delay Petri Net Based

RTD

Resistance Temperature Detector

FCFS

First Come, First Served \(Technique\)

SRTF

Shortest-Remaining-Time-First

MARL

Multi-Agent Reinforcement Learning

ACVAS

Advanced Cooperative Vehicle-Actuator System

LCS

Lane Control Signals

VSL

Variable Speed Limits

SUMO

Simulation Of Urban Mobility

MPV

Model Predictive Control

ALADIN

Augmented Lagrangian-Based Alternating Direction Inexact Newton

TTC

Time To Collision

MIQP

Mixed-Integer Quadratic Programming

CISP

Customized Synchronous Intersection Protocol

BRIP

Ballroom Intersection Protocol

AReBIC

Autonomous Reservation-Based Intersection Control

RL

Reinforcement Learning

RAAL

The Reserve Advance, Act Later

KNN

K-Nearest Neighbors

CS

Collision-Set

CARA

Collision-Aware Resource Allocation

QoS

Quality Of Service

TP-AIM

Trajectory Planning for Autonomous Intersection Management

DCL-AIM

Decentralized Coordination Learning of Autonomous Intersection Management VLC

Visible Light Communication

SICL

Signal-Head-Free Intersection Control Logic

CIC

Cooperative Intersection Control

SIoV

Social Internet of Vehicles

ENN

Elman Neural Network

SAA

Sparrow Search Algorithm

IoV

Internet of Vehicles

OP

Outage Probability

**References**

1. 

Alam, K.; Saini, M. Toward Social Internet of Vehicles: Concept, Architecture, and Applications. 2015. Available online:

https://ieeexplore.ieee.org/abstract/document/7067363/ \(accessed on 21 December 2022\). 

2. 

Rezapur-Shahkolai, F.; Afshari, M.; Doosti-Irani, A.; Bashirian, S.; Maleki, S. Interventions to Prevent Road Traffic Injuries among Pedestrians: A Systematic Review; Taylor & Francis: Abingdon, UK, 2022. \[CrossRef\]

Appl. Sci. **2023**, 13, 1789

23 of 27

3. 

Wang, Q.; Leng, S.; Fu, H.; Zhang, Y. An IEEE 802.11p-based multichannel MAC scheme with channel coordination for vehicular Ad hoc networks. IEEE Trans. Intell. Transp. Syst. **2012**, 13, 449–458. \[CrossRef\]

4. 

Zhou, H.; Chen, X.; He, S.; Chen, J.; Wu, J. DRAIM: A Novel Delay-Constraint and Reverse Auction-Based Incentive Mechanism for WiFi Offloading. IEEE J. Sel. Areas Commun. **2020**, 38, 711–722. \[CrossRef\]

5. 

Zhou, H.; Chen, X.; He, S.; Zhu, C.; Leung, V.C.M. Freshness-Aware Seed Selection for Offloading Cellular Traffic through Opportunistic Mobile Networks. IEEE Trans. Wirel. Commun. **2020**, 19, 2658–2669. \[CrossRef\]

6. 

Fakirah, M.; Leng, S.; Chen, X.; Zhou, J. Visible light communication-based traffic control of autonomous vehicles at multi-lane roundabouts. EURASIP J. Wirel. Commun. Netw. **2020**, 2020, 1–14. \[CrossRef\]

7. 

Barbaresso, J.; Cordahi, G.; Garcia, D.; Hill, C.; Jendzejec, A.; Wright, K.; Hamilton, B.A. USDOT’s Intelligent Transportation Systems \(ITS\) ITS Strategic Plan, 2015–2019. May 2014. Available online: https://ntl.bts.gov/ntl/public-access \(accessed on 21

December 2022\). 

8. 

Martin-Gasulla, M. Traffic Management with Autonomous and Connected Vehicles at Single-Lane Roundabouts. Available online: https://www.sciencedirect.com/science/article/pii/S0968090X21000024 \(accessed on 21 December 2022\). 

9. 

Jabbar, R.; Dhib, E.; Ben Said, A.; Krichen, M.; Fetais, N.; Zaidan, E.; Barkaoui, K. Blockchain Technology for Intelligent Transportation Systems: A Systematic Literature Review. IEEE Access **2022**, 10, 20995–21031. \[CrossRef\]

10. 

Rahmati, Y.; Talebpour, A. Towards a collaborative connected, automated driving environment: A game theory based decision framework for unprotected left turn maneuvers. In Proceedings of the IEEE Intelligent Vehicles Symposium, Los Angeles, LA, USA, 11–14 June 2017; pp. 1316–1321. \[CrossRef\]

11. 

Kerner, B.S. Effect of autonomous driving on traffic breakdown in mixed traffic flow: A comparison of classical ACC with three-traffic-phase-ACC \(TPACC\). Phys. A Stat. Mech. Appl. **2021**, 562, 125315. \[CrossRef\]

12. 

Dey, K.C.; Yan, L.; Wang, X.; Wang, Y.; Shen, H.; Chowdhury, M.; Yu, L.; Qiu, C.; Soundararaj, V. A Review of Communication, Driver Characteristics, and Controls Aspects of Cooperative Adaptive Cruise Control \(CACC\). IEEE Trans. Intell. Transp. Syst. 

**2016**, 17, 491–509. \[CrossRef\]

13. 

Kuutti, S.; Fallah, S.; Katsaros, K.; Dianati, M.; Mccullough, F.; Mouzakitis, A. A Survey of the State-of-the-Art Localization Techniques and Their Potentials for Autonomous Vehicle Applications. IEEE Internet Things J. **2018**, 5, 829–846. \[CrossRef\]

14. 

Onishi, H. A Survey: Why and How Automated Vehicles Should Communicate to Other Road-Users. In Proceedings of the IEEE

Vehicular Technology Conference, Chicago, IL, USA, 27–30 August 2018. \[CrossRef\]

15. 

Li, L.; Wen, D.; Yao, D. A survey of traffic control with vehicular communications. IEEE Trans. Intell. Transp. Syst. **2014**, 15, 425–432. \[CrossRef\]

16. 

Chen, L.; Englund, C. Cooperative Intersection Management: A Survey. IEEE Trans. Intell. Transp. Syst. **2016**, 17, 570–586. 

\[CrossRef\]

17. 

Silva, Ó.; Cordera, R.; González-González, E.; Nogués, S. Environmental impacts of autonomous vehicles: A review of the scientific literature. Sci. Total Environ. **2022**, 830, 154615. \[CrossRef\] \[PubMed\]

18. 

Rios-Torres, J.; Malikopoulos, A.A. A Survey on the Coordination of Connected and Automated Vehicles at Intersections and Merging at Highway On-Ramps. IEEE Trans. Intell. Transp. Syst. **2017**, 18, 1066–1077. \[CrossRef\]

19. 

Taylor, P.J.; Dargahi, T.; Dehghantanha, A.; Parizi, R.M.; Choo, K.K.R. A systematic literature review of blockchain cyber security. 

Digit. Commun. Netw. **2020**, 6, 147–156. \[CrossRef\]

20. 

Kitchenham, B.; Brereton, O.P.; Budgen, D.; Turner, M.; Bailey, J.; Linkman, S. Systematic literature reviews in software engineering—A systematic literature review. Inf. Softw. Technol. **2009**, 51, 7–15. \[CrossRef\]

21. 

Wohlin, C. Guidelines for snowballing in systematic literature studies and a replication in software engineering. In Proceedings of the ACM International Conference Proceeding Series, London, UK, 11–14 December 2014. \[CrossRef\]

22. 

Hosseini, S.; Turhan, B.; Gunarathna, D. A systematic literature review and meta-analysis on cross project defect prediction. IEEE

Trans. Softw. Eng. **2019**, 45, 111–147. \[CrossRef\]

23. 

Wuthishuwong, C.; Traechtler, A. Consensus-based local information coordination for the networked control of the autonomous intersection management. Complex. Intell. Syst. **2016**, 3, 17–32. \[CrossRef\]

24. 

Wu, J.; Abbas-Turki, A.; El Moudni, A. Cooperative driving: An ant colony system for autonomous intersection management. 

Appl. Intell. **2012**, 37, 207–222. \[CrossRef\]

25. 

De Campos, G.R.; Falcone, P.; Sjoberg, J. Autonomous cooperative driving: A velocity-based negotiation approach for intersection crossing. In Proceedings of the 16th International IEEE Conference on Intelligent Transportation Systems \(ITSC 2013\), The Hague, The Netherlands, 6–9 October 2013; pp. 1456–1461. \[CrossRef\]

26. 

Lu, Q.; Kim, K.D. Autonomous and connected intersection crossing traffic management using discrete-time occupancies trajectory. 

Appl. Intell. **2019**, 49, 1621–1635. \[CrossRef\]

27. 

Chai, L.; Cai, B.; Shangguan, W.; Wang, J. Connected and autonomous vehicles coordinating method at intersection utilizing preassigned slots. In Proceedings of the 2017 IEEE 20th International Conference on Intelligent Transportation Systems \(ITSC\), Yokohama, Japan, 16–19 October 2017; pp. 1–6. \[CrossRef\]

28. 

De Campos, G.R.; Falcone, P.; Hult, R.; Wymeersch, H.; Sjöberg, J. Traffic Coordination at Road Intersections: Autonomous Decision-Making Algorithms Using Model-Based Heuristics. IEEE Intell. Transp. Syst. Mag. **2017**, 9, 8–21. \[CrossRef\]

Appl. Sci. **2023**, 13, 1789

24 of 27

29. 

Zhang, K.; Yang, A.; Su, H.; de La Fortelle, A.; Wu, X. Unified modeling and design of reservation-based cooperation mechanisms for intelligent vehicles. In Proceedings of the 2016 IEEE 19th International Conference on Intelligent Transportation Systems \(ITSC\), Rio de Janeiro, Brazil, 1–4 November 2016; pp. 1192–1199. \[CrossRef\]

30. 

Aloufi, N.; Chatterjee, A. Autonomous Vehicle Scheduling at Intersections Based on Production Line Technique. In Proceedings of the IEEE Vehicular Technology Conference, Chicago, IL, USA, 27–30 August 2018. \[CrossRef\]

31. 

Du, G.; Zou, Y.; Zhang, X.; Dong, G.; Yin, X. Heuristic Reinforcement Learning Based Overtaking Decision for an Autonomous Vehicle. IFAC-Pap. **2021**, 54, 59–66. \[CrossRef\]

32. 

Lak, H.J.; Gholamhosseinian, A.; Seitz, J. Distributed Vehicular Communication Protocols for Autonomous Intersection Management. Procedia Comput. Sci. **2022**, 201, 150–157. \[CrossRef\]

33. 

Kamal, M.A.S.; Imura, J.I.; Hayakawa, T.; Ohata, A.; Aihara, K. A vehicle-intersection coordination scheme for smooth flows of traffic without using traffic lights. IEEE Trans. Intell. Transp. Syst. **2015**, 16, 1136–1147. \[CrossRef\]

34. 

Bashiri, M.; Jafarzadeh, H.; Fleming, C.H. PAIM: Platoon-based Autonomous Intersection Management. In Proceedings of the 2018 21st International Conference on Intelligent Transportation Systems \(ITSC\), Maui, HI, USA, 4–7 November 2018; pp. 374–380. 

\[CrossRef\]

35. 

Zhao, Y.; Yao, S.; Shao, H.; Abdelzaher, T. CoDrive: Cooperative driving scheme for vehicles in urban signalized intersections. In Proceedings of the 9th ACM/IEEE International Conference on Cyber-Physical Systems, ICCPS 2018, Porto, Portugal, 11–13 April 2018; pp. 308–319. \[CrossRef\]

36. 

Vrbanić, F.; Ivanjko, E.; Kušić, K.; Čakija, D. Variable Speed Limit and Ramp Metering for Mixed Traffic Flows: A Review and Open Questions. Appl. Sci. **2021**, 11, 2574. \[CrossRef\]

37. 

Perronnet, F.; Abbas-Turki, A.; el Moudni, A. Vehicle routing through deadlock-free policy for cooperative traffic control in a network of intersections: Reservation and congestion. In Proceedings of the 17th IEEE International Conference on Intelligent Transportation Systems, ITSC, Qingdao, China, 8–11 October 2014; pp. 2233–2238. \[CrossRef\]

38. 

Ma, Y.; Zhu, J. Left-turn conflict identification at signal intersections based on vehicle trajectory reconstruction under real-time communication conditions. Accid Anal. Prev. **2021**, 150, 105933. \[CrossRef\] \[PubMed\]

39. 

Vrbanić, F.; Ivanjko, E.; Mandžuka, S.; Miletić, M. Reinforcement learning based variable speed limit control for mixed traffic flows. In Proceedings of the 2021 29th Mediterranean Conference on Control and Automation \(MED\), Puglia, Italy, 21–25 June 2021; pp. 560–565. \[CrossRef\]

40. 

Vrbanić, F.; Tišljarić, L.; Majstorović, Ž.; Ivanjko, E. Reinforcement learning based variable speed limit control for mixed traffic flows using speed transition matrices for state estimation. In Proceedings of the 2022 30th Mediterranean Conference on Control and Automation \(MED\), Athens, Greece, 28 June–1 July 2022; pp. 1093–1098. \[CrossRef\]

41. 

Bitsch, G.; Schweitzer, F. Selection of optimal machine learning algorithm for autonomous guided vehicle’s control in a smart manufacturing environment. Procedia CIRP **2022**, 107, 1409–1414. \[CrossRef\]

42. 

Mihály, A.; Farkas, Z.; Zsuzsanna, B.; Gáspár, P. Performance Analysis of Model Predictive Intersection Control for Autonomous Vehicles. IFAC-Pap. **2021**, 54, 240–245. \[CrossRef\]

43. 

Fayazi, S.A.; Vahidi, A.; Luckow, A. Optimal scheduling of autonomous vehicle arrivals at intelligent intersections via MILP. In Proceedings of the American Control Conference, Seattle, WA, USA, 24–26 May 2017; pp. 4920–4925. \[CrossRef\]

44. 

Xie, X.F.; Wang, Z.J. SIV-DSS: Smart In-Vehicle Decision Support System for driving at signalized intersections with V2I communication. Transp. Res. Part C Emerg. Technol. **2018**, 90, 181–197. \[CrossRef\]

45. 

Mirheli, A.; Tajalli, M.; Hajibabai, L.; Hajbabaie, A. A consensus-based distributed trajectory control in a signal-free intersection. 

Transp. Res. Part C Emerg. Technol. **2019**, 100, 161–176. \[CrossRef\]

46. 

Vrbanić, F.; Miletić, M.; Tišljarić, L.; Ivanjko, E. Influence of Variable Speed Limit Control on Fuel and Electric Energy Consumption, and Exhaust Gas Emissions in Mixed Traffic Flows. Sustainability **2022**, 14, 932. \[CrossRef\]

47. 

Yamashita, T.; Kurumatani, K.; Izumi, K.; Nakashima, H. Smooth traffic flow with a cooperative car navigation system. In Proceedings of the International Conference on Autonomous Agents, Bologna, Italy, 6–11 July 2005; pp. 613–620. \[CrossRef\]

48. 

Zhang, Y.; Malikopoulos, A.A.; Cassandras, C.G. Decentralized optimal control for connected automated vehicles at intersections including left and right turns. In Proceedings of the 2017 IEEE 56th Annual Conference on Decision and Control, CDC 2017, Melbourne, Australia, 12–15 December 2017; pp. 4428–4433. \[CrossRef\]

49. 

Ding, H.; Pan, H.; Bai, H.; Zheng, X.; Chen, J.; Zhang, W. Driving strategy of connected and autonomous vehicles based on multiple preceding vehicles state estimation in mixed vehicular traffic. Phys. A Stat. Mech. Its Appl. **2022**, 596, 127154. \[CrossRef\]

50. 

Ding, J.; Xu, H.; Hu, J.; Zhang, Y. Centralized cooperative intersection control under automated vehicle environment. In Proceedings of the 2017 IEEE Intelligent Vehicles Symposium \(IV\), Los Angeles, CA, USA, 11–14 June 2017; pp. 972–977. 

\[CrossRef\]

51. 

Yan, F.; Dridi, M.; El Moudni, A. An autonomous vehicle sequencing problem at intersections: A genetic algorithm approach. Int. 

J. Appl. Math. Comput. Sci. **2013**, 23, 183–200. \[CrossRef\]

52. 

ShangGuan, W.; Yu, J.; Cai, B.; Wang, J. Research on Unsigned Intersection Control Method Based on Cooperative Vehicle Infrastructure System. Available online: https://ieeexplore.ieee.org/abstract/document/8243937/ \(accessed on 21 December 2022\). 

53. 

Elhenawy, M.; Elbery, A.A.; Hassan, A.A.; Rakha, H.A. An Intersection Game-Theory-Based Traffic Control Algorithm in a Connected Vehicle Environment. In Proceedings of the 2015 IEEE 18th International Conference on Intelligent Transportation Systems, Gran Canaria, Spain, 15–18 September 2015; pp. 343–347. \[CrossRef\]

Appl. Sci. **2023**, 13, 1789

25 of 27

54. 

Chen, B.; Sun, D.; Zhou, J.; Wong, W.; Ding, Z. A Future Intelligent Traffic System with Mixed Autonomous Vehicles and Human-Driven Vehicles. 2020. Available online: https://www.sciencedirect.com/science/article/pii/S0020025520300736 \(accessed on 21

December 2022\). 

55. 

Sala, M.; Soriguera, F. Capacity of a freeway lane with platoons of autonomous vehicles mixed with regular traffic. Transp. Res. 

Part B Methodol. **2021**, 147, 116–131. \[CrossRef\]

56. 

Li, S.; Shu, K.; Chen, C.; Cao, D. Planning and Decision-making for Connected Autonomous Vehicles at Road Intersections: A Review. Chin. J. Mech. Eng. **2021**, 34, 133. \[CrossRef\]

57. 

Gokasar, I.; Timurogullari, A.; Deveci, M.; Garg, H. SWSCAV: Real-time traffic management using connected autonomous vehicles. 

ISA Trans. **2022**, in press. \[CrossRef\]

58. 

Lu, G.; Li, L.; Wang, Y.; Zhang, R.; Bao, Z.; Chen, H. A rule based control algorithm of connected vehicles in uncontrolled intersection. In Proceedings of the 2014 17th IEEE International Conference on Intelligent Transportation Systems, ITSC 2014, Qingdao, China, 8–11 October 2014; pp. 115–120. \[CrossRef\]

59. 

Riegger, L.; Carlander, M.; Lidander, N.; Murgovski, N.; Sjöberg, J. Centralized MPC for autonomous intersection crossing. In Proceedings of the 2016 IEEE 19th International Conference on Intelligent Transportation Systems \(ITSC\), Rio de Janeiro, Brazil, 1–4 November 2016; pp. 1372–1377. \[CrossRef\]

60. 

Jiang, Y.; Zanon, M.; Hult, R.; Houska, B. Distributed Algorithm for Optimal Vehicle Coordination at Traffic Intersections. IFAC

**2017**, 50, 11577–11582. \[CrossRef\]

61. 

Németh, B.; Gáspár, P. Design of learning-based control with guarantees for autonomous vehicles in intersections. IFAC-Pap. 

**2021**, 54, 210–215. \[CrossRef\]

62. 

Khan, R.R.; Hanif, A.; Ahmed, Q. Cooperative Navigation Strategy for Connected Autonomous Vehicle Operating at Smart Intersection. IFAC-Pap. **2022**, 55, 279–284. \[CrossRef\]

63. 

Lamouik, I.; Yahyaouy, A.; Sabri, M.A. Smart multi-agent traffic coordinator for autonomous vehicles at intersections. In Proceedings of the 3rd International Conference on Advanced Technologies for Signal and Image Processing, ATSIP 2017, Fez, Morocco, 22–24 May 2017. \[CrossRef\]

64. 

Soto, I.; Calderon, M.; Amador, O.; Urueña, M. A survey on road safety and traffic efficiency vehicular applications based on C-V2X technologies. Veh. Commun. **2022**, 33, 100428. \[CrossRef\]

65. 

Gregoire, J.; Frazzoli, E. Hybrid centralized/distributed autonomous intersection control: Using a job scheduler as a planner and inheriting its efficiency guarantees. In Proceedings of the 2016 IEEE 55th Conference on Decision and Control, CDC 2016, Las Vegas, NV, USA, 12–14 December 2016; pp. 2549–2554. \[CrossRef\]

66. 

Mo, Y.; Wang, M.; Zhang, T.; Zhang, Q. Autonomous Cooperative Vehicle Coordination at Road Intersections. J. Commun. Inf. 

Netw. **2022**, 4, 78–87. \[CrossRef\]

67. 

Wang, M.; Zhang, T.; Gao, L.; Zhang, Q. High throughput dynamic vehicle coordination for intersection ground traffic. In Proceedings of the IEEE Vehicular Technology Conference, Chicago, IL, USA, 27–30 August 2018. \[CrossRef\]

68. 

González, C.L.; Pulido, J.J.; Alberola, J.M.; Julian, V.; Niño, L.F. Autonomous Distributed Intersection Management for Emergency Vehicles at Intersections. Commun. Comput. Inf. Sci. **2021**, 1472, 261–269. \[CrossRef\]

69. 

Xu, Y.; Zhou, H.; Qian, B.; Wu, H.; Zhang, Z.; Shen, X.S. When Automated Vehicles Meet Non-Signalized Intersections: A Collision-Free Scheduling Solution. In Proceedings of the 2018 IEEE/CIC International Conference on Communications in China, ICCC 2018, Beijing, China, 16–18 August 2018; pp. 709–713. \[CrossRef\]

70. 

Wang, Z.; Wu, G.; Hao, P.; Barth, M.J. Cluster-wise cooperative eco-approach and departure application along signalized arterials. 

In Proceedings of the 2017 IEEE 20th International Conference on Intelligent Transportation Systems \(ITSC\), Yokohama, Japan, 16–19 October 2017; pp. 145–150. \[CrossRef\]

71. 

Hacıo ˘glu, F. Power Consumption Based Multi Agent Intersection Management Method. 2017. Available online: https://

ieeexplore.ieee.org/abstract/document/8266343/ \(accessed on 21 December 2022\). 

72. 

Medina, A.I.M.; van de Wouw, N.; Nijmeijer, H. Cooperative Intersection Control Based on Virtual Platooning. IEEE Trans. Intell. 

Transp. Syst. **2018**, 19, 1727–1740. \[CrossRef\]

73. 

Bichiou, Y.; Rakha, H.A. Developing an Optimal Intersection Control System for Automated Connected Vehicles. IEEE Trans. 

Intell. Transp. Syst. **2019**, 20, 1908–1916. \[CrossRef\]

74. 

Zhao, L.; Malikopoulos, A.; Rios-Torres, J. Optimal Control of Connected and Automated Vehicles at Roundabouts: An Investigation in a Mixed-Traffic Environment. IFAC-Pap. **2018**, 51, 73–78. \[CrossRef\]

75. 

Krajewski, R.; Themann, P.; Eckstein, L. Decoupled cooperative trajectory optimization for connected highly automated vehicles at urban intersections. In Proceedings of the 2016 IEEE Intelligent Vehicles Symposium \(IV\), Gotenburg, Sweden, 19–22 June 2016; pp. 741–746. \[CrossRef\]

76. 

Mladenovic, M.N.; Abbas, M.M. Self-organizing control framework for driverless vehicles. In Proceedings of the 16th International IEEE Conference on Intelligent Transportation Systems \(ITSC 2013\), The Hague, The Netherlands, 6–9 October 2013; pp. 2076–2081. 

\[CrossRef\]

77. 

Xu, L.; Zhou, X.; Khan, M.A.; Li, X.; Menon, V.G.; Yu, X. Communication Quality Prediction for Internet of Vehicle \(IoV\) Networks: An Elman Approach. IEEE Trans. Intell. Transp. Syst. **2022**, 23, 19644–19654. \[CrossRef\]

78. 

Cao, Z.; Guo, H.; Zhang, J.; Niyato, D.; Fastenrath, U. Improving the efficiency of stochastic vehicle routing: A partial lagrange multiplier method. IEEE Trans. Veh. Technol. **2016**, 65, 3993–4005. \[CrossRef\]

Appl. Sci. **2023**, 13, 1789

26 of 27

79. 

Deveci, M.; Pamucar, D.; Gokasar, I. Fuzzy Power Heronian function based CoCoSo method for the advantage prioritization of autonomous vehicles in real-time traffic management. Sustain. Cities Soc. **2021**, 69, 102846. \[CrossRef\]

80. 

Cao, Z.; Guo, H.; Zhang, J. A Multiagent-Based Approach for Vehicle Routing by Considering Both Arriving on Time and Total Travel Time. ACM Trans. Intell. Syst. Technol. **2017**, 9, 8847. \[CrossRef\]

81. 

Jiang, S.; Zhang, J.; Ong, Y.-S. A Pheromone-Based Traffic Management Model for Vehicle Re-Routing and Traffic Light Control \(Extended Abstract\). Available online: www.ifaamas.org \(accessed on 21 December 2022\). 

82. 

Yu, C.; Tan, G.; Yu, Y. Make driver agent more reserved: An AIM-based incremental data synchronization policy. In Proceedings of the IEEE 9th International Conference on Mobile Ad-Hoc and Sensor Networks, MSN, Dalian, China, 11–13 December 2013; pp. 198–205. \[CrossRef\]

83. 

Zhang, K.; De La Fortelle, A.; Zhang, D.; Wu, X. Analysis and Modeled Design of One State-Driven Autonomous Passing-Through Algorithm for Driverless Vehicles at Intersections. 2013. Available online: https://ieeexplore.ieee.org/abstract/document/6755

295/ \(accessed on 21 December 2022\). 

84. 

Zhang, K.; Yang, A.; Su, H.; de La Fortelle, A.; Miao, K.; Yao, Y. Service-Oriented Cooperation Models and Mechanisms for Heterogeneous Driverless Vehicles at Continuous Static Critical Sections. 2016. Available online: https://ieeexplore.ieee.org/

abstract/document/7725527/ \(accessed on 21 December 2022\). 

85. 

Andert, E.; Khayatian, M.; Shrivastava, A. Crossroads: Time-sensitive autonomous intersection management technique. In Proceedings of the 54th Annual Design Automation Conference, Austin, TX, USA, 18–22 June 2017. \[CrossRef\]

86. 

Wei, X.; Tan, G.; Ding, N. Batch-light: An adaptive intelligent intersection control policy for autonomous vehicles. In Proceedings of the 2014 IEEE International Conference on Progress in Informatics and Computing, Shanghai, China, 16–18 May 2014; pp. 

98–103. Available online: https://ieeexplore.ieee.org/abstract/document/6728285/ \(accessed on 21 December 2022\). 

87. 

Shivam, S.; Wardi, Y.; Egerstedt, M.; Kanellopoulos, A.; Vamvoudakis, K.G. Intersection-Traffic Control of Autonomous Vehicles using Newton-Raphson Flows and Barrier Functions. 2020. Available online: https://www.sciencedirect.com/science/article/

pii/S2405896320303086 \(accessed on 21 December 2022\). 

88. 

Wang, J.; Lv, W.; Jiang, Y.; Qin, S.; Li, J. A multi-agent based cellular automata model for intersection traffic control simulation. 

Phys. A Stat. Mech. Its Appl. **2021**, 584, 126356. \[CrossRef\]

89. 

Zhou, W.; Chen, D.; Yan, J.; Li, Z.; Yin, H.; Ge, W. Multi-agent reinforcement learning for cooperative lane changing of connected and autonomous vehicles in mixed traffic. Auton. Intell. Syst. **2022**, 2, 1–11. \[CrossRef\]

90. 

Miglani, A.; Kumar, N. Deep learning models for traffic flow prediction in autonomous vehicles: A review, solutions, and challenges. Veh. Commun. **2019**, 20, 100184. \[CrossRef\]

91. 

Ma, M.; Li, Z. A time-independent trajectory optimization approach for connected and autonomous vehicles under reservation-based intersection control. Transp. Res. Interdiscip. Perspect. **2021**, 9, 100312. \[CrossRef\]

92. 

Belkhouche, F. Control of autonomous vehicles at an unsignalized intersection. In Proceedings of the American Control Conference, Seattle, WA, USA, 24–26 May 2017; pp. 1340–1345. \[CrossRef\]

93. 

Altché, F.; Qian, X.; de La Fortelle, A. Least restrictive and minimally deviating supervisor for safe semi-Autonomous driving at an intersection: An MIQP approach. In Proceedings of the 2016 IEEE 19th International Conference on Intelligent Transportation Systems \(ITSC\), Rio de Janeiro, Brazil, 1–4 November 2016; pp. 2520–2526. \[CrossRef\]

94. 

Patil, S.; Raju, N.; Arkatkar, S.S.; Easa, S. Modeling vehicle collision instincts over road midblock using deep learning. J. Intell. 

Transp. Syst. **2021**, 2021, 1–15. \[CrossRef\]

95. 

Aoki, S.; Rajkumar, R. A configurable synchronous intersection protocol for self-driving vehicles. In Proceedings of the RTCSA 2017—23rd IEEE International Conference on Embedded and Real-Time Computing Systems and Applications, Hsinchu, Taiwan, 16–18 August 2017. \[CrossRef\]

96. 

Savic, V.; Schiller, E.M.; Papatriantafilou, M. Distributed algorithm for collision avoidance at road intersections in the presence of communication failures. In Proceedings of the 2017 IEEE Intelligent Vehicles Symposium \(IV\), Los Angeles, CA, USA, 11–14 June 2017; pp. 1005–1012. \[CrossRef\]

97. 

Chang, Y.; Edara, P. AReBIC: Autonomous reservation-based intersection control for emergency evacuation. In Proceedings of the 2017 IEEE Intelligent Vehicles Symposium \(IV\), Los Angeles, CA, USA, 11–14 June 2017; pp. 1887–1892. \[CrossRef\]

98. 

Haseeb, K.; Rehman, A.; Saba, T.; Bahaj, S.A.; Wang, H.; Song, H. Efficient and trusted autonomous vehicle routing protocol for 6G networks with computational intelligence. ISA Trans. **2022**, in press. \[CrossRef\] \[PubMed\]

99. 

Zheng, B.; Lin, C.W.; Liang, H.; Shiraishi, S.; Li, W.; Zhu, Q. Delay-Aware design, analysis and verification of intelligent intersection management. In Proceedings of the 2017 IEEE International Conference on Smart Computing, SMARTCOMP 2017, Hong Kong, China, 29–31 May 2017. \[CrossRef\]

100. Chouhan, A.P.; Banda, G. Autonomous intersection management: A heuristic approach. IEEE Access **2018**, 6, 53287–53295. 

\[CrossRef\]

101. Creemers, F.; Medina, A.I.M.; Lefeber, E.; van de Wouw, N. Design of a supervisory controller for Cooperative Intersection Control using Model Predictive Control. IFAC-Pap. **2018**, 51, 74–79. \[CrossRef\]

102. Liu, C.; Lin, C.W.; Shiraishi, S.; Tomizuka, M. Distributed Conflict Resolution for Connected Autonomous Vehicles. IEEE Trans. 

Intell. Veh. **2018**, 3, 18–29. \[CrossRef\]

103. Lu, Q.; Kim, K.D. A mixed integer programming approach for autonomous and connected intersection crossing traffic control. In Proceedings of the IEEE Vehicular Technology Conference, Chicago, IL, USA, 27–30 August 2018. \[CrossRef\]

Appl. Sci. **2023**, 13, 1789

27 of 27

104. Steinmetz, E.; Hult, R.; Zou, Z.; Emardson, R.; Brännström, F.; Falcone, P.; Wymeersch, H. Collision-aware communication for intersection management of automated vehicles. IEEE Access **2018**, 6, 77359–77371. \[CrossRef\]

105. Wei, H.; Mashayekhy, L.; Papineau, J. Intersection management for connected autonomous vehicles: A game theoretic framework. 

In Proceedings of the 2018 21st International Conference on Intelligent Transportation Systems \(ITSC\), Maui, HI, USA, 4–7

November 2018; pp. 583–588. \[CrossRef\]

106. Cruz-Piris, L.; Lopez-Carmona, M.A.; Marsa-Maestre, I. Automated Optimization of Intersections Using a Genetic Algorithm. 

IEEE Access **2019**, 7, 15452–15468. \[CrossRef\]

107. Liu, B.; Shi, Q.; Song, Z.; el Kamel, A. Trajectory planning for autonomous intersection management of connected vehicles. Simul. 

Model. Pract. Theory **2019**, 90, 16–30. \[CrossRef\]

108. Wu, Y.; Chen, H.; Zhu, F. DCL-AIM: Decentralized coordination learning of autonomous intersection management for connected and automated vehicles. Transp. Res. Part C Emerg. Technol. **2019**, 103, 246–260. \[CrossRef\]

109. He, Z.; Zheng, L.; Lu, L.; Guan, W. Erasing Lane Changes from Roads: A Design of Future Road Intersections. IEEE Trans. Intell. 

Veh. **2018**, 3, 173–184. \[CrossRef\]

110. Liu, Y.; Gao, Y.; Zhang, Q.; Ding, D.; Zhao, D. Multi-task safe reinforcement learning for navigating intersections in dense traffic. 

J. Frankl. Inst. **2022**, in press. \[CrossRef\]

111. Xu, B.; Ban, X.J.; Bian, Y.; Wang, J.; Li, K. V2I based cooperation between traffic signal and approaching automated vehicles. In Proceedings of the IEEE Intelligent Vehicles Symposium, Los Angeles, LA, USA, 11–14 June 2017; pp. 1658–1664. \[CrossRef\]

112. Gholamhosseinian, A.; Seitz, J. A Comprehensive Survey on Cooperative Intersection Management for Heterogeneous Connected Vehicles. IEEE Access **2022**, 10, 7937–7972. \[CrossRef\]

113. Mirheli, A.; Hajibabai, L.; Hajbabaie, A. Development of a signal-free intersection control logic in a fully connected and autonomous vehicle environment. In Proceedings of the Transportation Research Board 97th Annual Meeting, Wahington, DC, USA, 7–11 January 2018. 

114. Malikopoulos, A.A.; Cassandras, C.G.; Zhang, Y.J. A decentralized energy-optimal control framework for connected automated vehicles at signal-free intersections. Automatica **2018**, 93, 244–256. \[CrossRef\]

115. Philip, B.V.; Alpcan, T.; Jin, J.; Palaniswami, M. Distributed Real-Time IoT for Autonomous Vehicles. IEEE Trans. Ind. Inf. **2019**, 15, 1131–1140. \[CrossRef\]

116. Xu, B.; Ban, X.J.; Bian, Y.; Li, W.; Wang, J.; Li, S.E.; Li, K. Cooperative Method of Traffic Signal Optimization and Speed Control of Connected Vehicles at Isolated Intersections. IEEE Trans. Intell. Transp. Syst. **2019**, 20, 1390–1403. \[CrossRef\]

117. Dai, P.; Liu, K.; Zhuge, Q.; Sha, E.H.M.; Lee, V.C.S.; Son, S.H. Quality-of-Experience-Oriented Autonomous Intersection Control in Vehicular Networks. IEEE Trans. Intell. Transp. Syst. **2016**, 17, 1956–1967. \[CrossRef\]

118. Roopa, M.S.; Siddiq, S.A.; Buyya, R.; Venugopal, K.R.; Iyengar, S.S.; Patnaik, L.M. DTCMS: Dynamic traffic congestion management in Social Internet of Vehicles \(SIoV\). Internet Things **2021**, 16, 100311. \[CrossRef\]

**Disclaimer/Publisher’s Note: **The statements, opinions and data contained in all publications are solely those of the individual author\(s\) and contributor\(s\) and not of MDPI and/or the editor\(s\). MDPI and/or the editor\(s\) disclaim responsibility for any injury to people or property resulting from any ideas, methods, instructions or products referred to in the content. 



# Document Outline

+ Introduction   
	+ Prior Research  
	+ Research Goal  
	+ Contribution and Layout  

+ Research Methodology   
	+ Primary Studies Selection  
	+ Inclusion and Exclusion Criteria  
	+ Selection Results  
	+ Quality Assesment  
	+ Data Extraction  
	+ Data Analysis   
		+ Publication Overtime  
		+ Substantial Keyword Distribution  


+ Research Analysis   
	+ Driving Objectives Perspective  
	+ Traffic Management Methodologies Consisiting of Primary Goals   
		+ Efficiency  
		+ Safety  
		+ Safety and Efficiency  
		+ Efficiency and Ecology  
		+ Ecology, Passenger Comfort, and Safety  
		+ Efficiency, Safety, and Ecology  
		+ Efficiency, Safety, and Passenger Comfort  
		+ Efficiency, Safety, Ecology, and Passenger Comfort  
		+ Other: Data Sharing  


+ Discussion  
+ Conclusions  
+ References



