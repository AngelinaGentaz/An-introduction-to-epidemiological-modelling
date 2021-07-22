# 1 Introduction
## 1.1 Context

In the current context of the Covid-19 outbreak, modelling the number of cases and the evolution of a disease is becoming essential to predict and anticipate the situation, and act accordingly. To better understand this, we will look at the case of seasonal influenza. We will begin by describing the main characteristics of this disease.

Seasonal influenza is an acute contagious respiratory infection caused by influenza viruses, which are characterized by high genetic variability. There are three types of seasonal influenza infecting humans: A, B and C. Types A and B are responsible for seasonal epidemics, and only type A influenza viruses have caused pandemics. Infection is usually characterised by signs of difficulty breathing, fever, muscle aches and headaches. Simple treatment can be effective and leads to a rapid recovery. Some frail people are nevertheless at risk of developing severe influenza which may require hospitalisation in intensive care or even ventilatory assistance.

According to the Red Cross, an epidemic is defined as "an anormal increase in the number of cases of an infectious disease, which exists in an endemic state, in a given area or population. It may also be the occurrence of a large number of cases of an infectious disease in an area or population that is normally free of it.
Annual seasonal epidemics are a public health issue because they affect millions of people in France each year, with possible mortality mainly in fragile subjects. Moreover, the permanent possibility of antigenic drift implies that it is necessary to reformulate seasonal influenza vaccines every year.

## 1.2 Objectives

The spread of an infectious agent in a population is a dynamic phenomenon. Many epidemiological models have been developed and have played a role in political and health decisions. But on what parameters are these models based? Are they sufficient to qualify as an "epidemiological" policy? In order to answer these questions, we propose in this report to describe an epidemiological model, to study it for a seasonal influenza epidemic, to define its characteristics, its advantages and disadvantages. A section will present the methodology that we applied in the choice of the model and the data as well as an explanation of the least squares method.

Our objectives will be to model its dynamics and characteristics, such as the peak and decay of the phenomenon, and then to estimate the different parameters of the infection using a mathematical resolution. To do this, we will detail the method used by presenting our chosen model and our dataset. Secondly, we will present and explain the results obtained from our modelling. Finally, we will discuss the effectiveness of the techniques that allowed us to gather our results and build our work in order to conclude this study.

# 2 Epidemiological models description
## 2.1 Model classification

Currently, mathematical models can be divided into three main categories: (1) statistical, (2) mechanistic and (3) empirical/automatic learning (Figure 1).

![Figure 1 :Overview of mathematical models for infectious diseases (from Siettos and Russo, 2013)](https://user-images.githubusercontent.com/85577140/126706328-60db96be-c407-4d03-9a0e-f786bc482d1f.jpg)

Figure 1 :Overview of mathematical models for infectious diseases (from Siettos and Russo, 2013)

*Note on deterministic continuum models* : expressed as differential and/or partial differential equations. They describe the overall dynamics of epidemics in a given population. The best representative of this model is the one developed by Kermack and McKendrick (1927): the compartmental SIR (susceptible, infected, recovered) model, which we will develop further.

*Note on stochastic models* : models at the individual level with the assumption of mean-field approximations of an infinite population and a perfect mixture (individual behaviour and multiple heterogeneous characteristics). The main representative is discrete Markov chains where time and states are defined over a discrete set of values.

## 2.2 SIR and SEIR model

As mentioned above, deterministic continuum models are mainly represented by the Kermack-McKendrick (SIR) model of 1927. The derived equations and assumptions are described below.

![Figure 2](https://user-images.githubusercontent.com/85577140/126707666-7a86e96a-4d7e-49ae-be27-da4d1a4a2758.jpg)

The differential equations for this model are :

![Figure 3](https://user-images.githubusercontent.com/85577140/126708647-89349656-7199-4023-837b-455da485f056.jpg)

where β represents the rate of infection and γ the rate of cure. β corresponds in fact to the probability of being infected after having been in contact with an infected individual. The latter varies somewhat according to the virus considered but depends mainly on the environment, hence a value which can easily vary between 0.2 and 0.8. γ corresponds in fact to the probability of no longer being able to transmit the virus, either after being immunised or after death.

The SIR model can be modified to incorporate another variable, which is the "exposed compartment" (SEIR model) as in Figure 3 (Brauer, 2008).

![Figure 4](https://user-images.githubusercontent.com/85577140/126707728-bb428c12-2a81-4f1c-8a11-5413c9909c19.jpg)

The differential equations for this model are :

![Figure 4](https://user-images.githubusercontent.com/85577140/126708869-9b44da95-568d-4102-81c9-a75890b0e425.jpg)

where, as we have seen above, β represents the infection rate and γ the cure rate. Added to these two parameters, $\alpha$ which corresponds to the incubation rate, ν which corresponds to the birth rate, μ which corresponds to the mortality rate. Finally N(t) corresponds to the total population which evolves during the time t. We realise that the SEIR model is a little more elaborate: it takes into account three more hypotheses than the SIR model, the demography of the population in particular.

*Note on the basic reproduction rate R0*:
Sometimes called the base number, the R0 can be described as the reproduction rate of the virus, or the average number of people infected following the arrival of a single infectious individual in a population where all individuals are susceptible to the infectious agent. Before being used in epidemiology, this concept was originally used in demography. The R0 is a dynamic variable that represents a picture at a given time of virus transmission in a given context. It depends on three parameters and is calculated in this way (Van den Driessche, 2017):

R0 = pcd

where p is the probability of transmission of the virus, c is the number of daily contacts and d is the duration of the illness.
For influenza, it is about 1.5. In other words, one person infected with influenza at the beginning of the epidemic will infect an average of 1 to 2 others. To prevent the epidemic from growing, the $R_{0}$ must remain below 1. This breaks the chains of transmission and thus reduces the number of cases at each "generation" of the epidemic. When the R0 is greater than 1, this means that each infection causes more than one new infection and therefore the situation can evolve rapidly from a cluster to an epidemic or even a pandemic (examples with H1N1 and Covid-19). However, during our modelling, we will not need this data. Indeed, the SIR model, which is rather simplified, does not take into account the R0 parameters.

# 3 Methodology
## 3.1 Model selection

After having familiarised ourselves with the different epidemiological models existing in the literature as explained above, we decided to run the SIR model on Excel. Our objective is to be able to compare real data found on the influenza epidemic with this model and thus discuss its relevance. The SIR model, which is quite simple and intuitive, seemed to us to be the ideal starting point for a first overview. The starting hypotheses are as follows:
* Constant homogeneous population (no account taken of births and deaths)
* Each individual has an equal probability of transmission and an equal degree of vulnerability 
* Only one type of virus in circulation
* Other environmental factors are neglected

## 3.2 Choice of the dataset

To carry out our project, we searched the internet for a dataset that would allow us to test our SIR model with reality. To do this, the dataset had to include :
* The number of infected for each period Δt
* A fairly long period (at least 5 years) as influenza is seasonal, so we needed to observe at least one peak but ideally more than one (for sampling concerns) to best understand what the data represented 

After much research, the data provided by the Sentinel network seemed to be the most reliable and relevant. We then had to "clean up" the data set. Indeed, the data provided went from 1985 to 2020 !

## 3.3 Least squares method

The method of least squares makes it possible to compare experimental data, which are generally affected by measurement errors, with a mathematical model that is supposed to describe these data. Mathematically, it is translated as follows :

min $\sum[y_{obs,i}-y_{théo}(x_{i})]^2$

The use of this method allows the model to be optimised: this is known as least squares model fitting. We will discuss the use of this method in the context of our modelling in the Results section.

# 4 Results




