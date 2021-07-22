# 1 Introduction
## 1.1 Context

In the current context of the Covid-19 outbreak, modelling the number of cases and the evolution of a disease is becoming essential to predict and anticipate the situation, and act accordingly. To better understand this, we will look at the case of seasonal influenza. We will begin by describing the main characteristics of this disease.

Seasonal influenza is an acute contagious respiratory infection caused by influenza viruses, which are characterized by high genetic variability. There are three types of seasonal influenza infecting humans: A, B and C. Types A and B are responsible for seasonal epidemics, and only type A influenza viruses have caused pandemics. Infection is usually characterised by signs of difficulty breathing, fever, muscle aches and headaches. Simple treatment can be effective and leads to a rapid recovery. Some frail people are nevertheless at risk of developing severe influenza which may require hospitalisation in intensive care or even ventilatory assistance.

According to the Red Cross, an epidemic is defined as "an abnormal increase in the number of cases of an infectious disease, which exists in an endemic state, in a given area or population. It may also be the occurrence of a large number of cases of an infectious disease in an area or population that is normally free of it.
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

## 2.2 SIR ans SEIR model

As mentioned above, deterministic continuum models are mainly represented by the Kermack-McKendrick (SIR) model of 1927. The derived equations and assumptions are described below.

![Figure 2](https://user-images.githubusercontent.com/85577140/126707666-7a86e96a-4d7e-49ae-be27-da4d1a4a2758.jpg)

The differential equations for this model are :

![Figure 3](https://user-images.githubusercontent.com/85577140/126708647-89349656-7199-4023-837b-455da485f056.jpg)

where $\beta$ represents the rate of infection and $\gamma$ the rate of cure. $\beta$ corresponds in fact to the probability of being infected after having been in contact with an infected individual. The latter varies somewhat according to the virus considered but depends mainly on the environment, hence a value which can easily vary between 0.2 and 0.8. $\gamma$ corresponds in fact to the probability of no longer being able to transmit the virus, either after being immunised or after death.

The SIR model can be modified to incorporate another variable, which is the "exposed compartment" (SEIR model) as in Figure 3 (Brauer, 2008).

![Figure 4](https://user-images.githubusercontent.com/85577140/126708869-9b44da95-568d-4102-81c9-a75890b0e425.jpg)

The differential equations for this model are :

\begin{center}
   $\left\{\begin{array}{l}
\frac{d S(t)}{d t}=-\beta S(t) I(t)+\nu N(t)-\mu S(t) \\
\frac{d E(t)}{d t}=\beta S(t) I(t)-\alpha E(t)-\mu(t) \\
\frac{d I(t)}{d t}=\alpha E(t)-\gamma I(t)-\mu I(t) \\
\frac{d R(t)}{d t}=\gamma I(t)-\mu R(t)
\end{array}\right.$
\end{center}




