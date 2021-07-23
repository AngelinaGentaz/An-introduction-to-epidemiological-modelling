# An introduction to epidemiological modelling

Project carried out as part of a first-year degree at Sorbonne University with Bonnet Sophie, Delcourt Oriane, Eberwein Johann, students in the PCGI portal at Sorbonne University (2020-2021 academic year)

# 1 Introduction
## 1.1 Context

In the current context of the Covid-19 outbreak, modelling the number of cases and the evolution of a disease is becoming essential to predict and anticipate the situation, and act accordingly. To better understand this, we will look at the case of seasonal influenza. We will begin by describing the main characteristics of this disease.

Seasonal influenza is an acute contagious respiratory infection caused by influenza viruses, which are characterized by high genetic variability. There are three types of seasonal influenza infecting humans: A, B and C. Types A and B are responsible for seasonal epidemics, and only type A influenza viruses have caused pandemics. Infection is usually characterised by signs of difficulty breathing, fever, muscle aches and headaches. Simple treatment can be effective and leads to a rapid recovery. Some frail people are nevertheless at risk of developing severe influenza which may require hospitalisation in intensive care or even ventilatory assistance.

According to the Red Cross, an epidemic is defined as an anormal increase in the number of cases of an infectious disease, which exists in an endemic state, in a given area or population. It may also be the occurrence of a large number of cases of an infectious disease in an area or population that is normally free of it. Annual seasonal epidemics are a public health issue because they affect millions of people in France each year, with possible mortality mainly in fragile subjects. Moreover, the permanent possibility of antigenic drift implies that it is necessary to reformulate seasonal influenza vaccines every year.

## 1.2 Objectives

The spread of an infectious agent in a population is a dynamic phenomenon. Many epidemiological models have been developed and have played a role in political and health decisions. But on what parameters are these models based? Are they sufficient to qualify as an "epidemiological" policy ? In order to answer these questions, we propose in this report to describe an epidemiological model, to study it for a seasonal influenza epidemic, to define its characteristics, its advantages and disadvantages. A section will present the methodology that we applied in the choice of the model and the data as well as an explanation of the least squares method.

Our objectives will be to model its dynamics and characteristics, such as the peak and decay of the phenomenon, and then to estimate the different parameters of the infection using a mathematical resolution. To do this, we will detail the method used by presenting our chosen model and our dataset. Secondly, we will present and explain the results obtained from our modelling. Finally, we will discuss the effectiveness of the techniques that allowed us to gather our results and build our work in order to conclude this study.

# 2 Epidemiological models description
## 2.1 Model classification

Currently, mathematical models can be divided into three main categories: (1) statistical, (2) mechanistic and (3) empirical/automatic learning (Figure 1).

![Figure 1 :Overview of mathematical models for infectious diseases (from Siettos and Russo, 2013)](https://user-images.githubusercontent.com/85577140/126706328-60db96be-c407-4d03-9a0e-f786bc482d1f.jpg)

Figure 1 :Overview of mathematical models for infectious diseases (from Siettos and Russo, 2013)

*Note on deterministic continuum models* : expressed as differential and/or partial differential equations. They describe the overall dynamics of epidemics in a given population. The best representative of this model is the one developed by Kermack and McKendrick (1927): the compartmental SIR (susceptible, infected, recovered) model, which we will develop further.

*Note on stochastic models* : models at the individual level with the assumption of mean-field approximations of an infinite population and a perfect mixture (individual behaviour and multiple heterogeneous characteristics). The main representative is discrete Markov chains where time and states are defined over a discrete set of values.

## 2.2 SIR and SEIR model

As mentioned above, deterministic continuum models are mainly represented by the Kermack-McKendrick (SIR) model of 1927. The flow chart for the SIR model looks like this:

![Figure 2](https://user-images.githubusercontent.com/85577140/126707666-7a86e96a-4d7e-49ae-be27-da4d1a4a2758.jpg)

The differential equations for this model are :

![Figure 3](https://user-images.githubusercontent.com/85577140/126708647-89349656-7199-4023-837b-455da485f056.jpg)

Susceptible individuals become infected at rate β, and infected individuals recover at rate γ. The last equation can be omitted if N is kept fixed, and R can be deduced from R(t) = N − S(t) − I(t).
The infection rate β is defined as the product of the average number of contacts each individual makes per unit time, c, and the probability of infection via contact, p, divided by the total population size, N :

![Figure 4](https://user-images.githubusercontent.com/85577140/126776508-b988b8df-998f-4ce4-b3b0-c885bf193ebb.jpg)

The recovery rate γ is simply the inverse of the characteristic timescale over which an individual remains infected T :

![Figure 4](https://user-images.githubusercontent.com/85577140/126776479-60a2a760-fc0e-47a0-9fcc-1000a7978514.jpg)

The SIR model can be modified to incorporate another variable, which is the "exposed compartment" (SEIR model) as in Figure 3 (Brauer, 2008) and the flow chart for the SEIR model looks like this:

![Figure 4](https://user-images.githubusercontent.com/85577140/126707728-bb428c12-2a81-4f1c-8a11-5413c9909c19.jpg)

The differential equations for this model are :

![Figure 4](https://user-images.githubusercontent.com/85577140/126708869-9b44da95-568d-4102-81c9-a75890b0e425.jpg)

α corresponds to the incubation rate, ν corresponds to the birth rate, μ corresponds to the mortality rate. Finally N(t) corresponds to the total population which evolves during the time t. We realise that the SEIR model is a little more elaborate: it takes into account three more hypotheses than the SIR model, the demography of the population in particular.

*Note on the basic reproduction rate R0*:
Sometimes called the base number, the R0 can be described as the reproduction rate of the virus, or the average number of people infected following the arrival of a single infectious individual in a population where all individuals are susceptible to the infectious agent. Before being used in epidemiology, this concept was originally used in demography. The R0 is a dynamic variable that represents a picture at a given time of virus transmission in a given context. It depends on three parameters and is calculated in this way (Van den Driessche, 2017):

R0 = p.c.d

where, as we have seen above, p is the probability of infection via contact, c is the average number of contacts each individual makes per unit time and d is the duration of the illness.
For influenza, it is about 1.7. To prevent the epidemic from growing, the R0 must remain below 1. This breaks the chains of transmission and thus reduces the number of cases at each "generation" of the epidemic. When the R0 is greater than 1, this means that each infection causes more than one new infection and therefore the situation can evolve rapidly from a cluster to an epidemic or even a pandemic (examples with H1N1 and Covid-19). However, during our modelling, we will not need this data. 

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

![Figure 4](https://user-images.githubusercontent.com/85577140/126714687-d3302316-93f6-4935-9b56-a88c59042354.jpg)

The use of this method allows the model to be optimised: this is known as least squares model fitting. We will discuss the use of this method in the context of our modelling in the Results section.

# 4 Results

In a first step we modelled our SIR model via Excel. I plan to publish the Python program on github but you can send me a private message if you are interested in having it before. 
The three initial compartments (Sucpetible, Infected and Recovered) could thus be set up. Once the formulas were entered into the Excel cells, it was interesting to compare the modelling with our real data. To do this, we proceeded as follows on 3 of the peaks already identified in our real data from the Sentinel network :
* The initial infection rate at the beginning of the epidemic peak is taken from the data.
* This is entered into the first cell of the Infected column. In this way, the model and the actual data start from the same initial infection rate at time t=0. This allows us to see, for example, if the model will reach the epidemic peak faster than the real data or vice versa.
* We plot the two corresponding curves (one corresponding to our epidemic peak from the real data and the other from our modelling) on the same graph for easy comparison.

In order to further fit our model with the real data, as discussed in the Methodology section, we then apply the least squares method:
* Having previously identified how many Excel cells were affected by our epidemic peak from the real data, we calculate the difference between the rate of infection at time t in our modelling and the rate of infection at time t in our epidemic peak from the real data.
* Sum the squares of these differences.
* Apply the Solver tool of Excel.

Let us now introduce the graphs found. For the first epidemiological peak studied, we have :

![Pic1](https://user-images.githubusercontent.com/85577140/126783914-9c4a4c18-5ffa-4424-aaa4-7c767ddb5546.jpg)
![Pic1MMC](https://user-images.githubusercontent.com/85577140/126794907-1f0dc9af-9dff-4df3-b809-e667cde0ee21.jpg)

We can immediately notice the efficiency of the least squares method: our model is much more adjusted to reality when we apply this method. The Solver tool in Excel was able to modify the value of the β and γ parameters by taking into account the different formulas entered in the cells. For the minimisation of the square of the deviations, we find the figure of about 0.000001 (see Excel file in the rest of the repo).

A first remark that we can make is that our model is very sensitive to the β and γ parameters and this to the nearest hundredth. Indeed, without applying the method of least squares and by choosing β = 0,8 and β = 0,7 , apart from the direction of variation, the curves do not look very similar. However, a small variation in the value of the parameters β and γ (of the order of a hundredth, as we end up with beta = 0.826 and gamma= 0,762), leads to a different result where the growth and decay of the two curves are similar and the epidemiological peak is almost reached at the same time (around the 6th week). The difference between the infection rate of the first and the second curve is almost zero for each week, which shows that the least squares method allowed us to fit our model to the real life data. 

Now, let us consider a second epidemiological peak.

![Pic2](https://user-images.githubusercontent.com/85577140/126783927-06a7ecf6-649b-4aec-b00b-dd473fcf0985.jpg)
![Pic2MMC](https://user-images.githubusercontent.com/85577140/126784278-3886d3f9-6e01-41ea-ae10-5e3d5a2678d5.jpg)

For the minimisation of the square of the deviations, we find the figure of about 0.00001 (see Excel file in the rest of the repo).

This time, rather than the flatten shape of the curve representing the real data (see the very first graph) which would mean that the model does not fit reality very well, it is more the moment when the epidemic peak is reached that is problematic (reached at the 7th week with our model versus at the 9th in reality). The growth and decay times start earlier with our model which gives this "shifted" effect of the curve representing the real data. However, by applying again the least squares method, this "shifted" effect disappears.  Our model is similar to a bell curve whereas the curve representing the real data has a slightly more pronounced exponential growth and decay. The epidemic peak is reached at exactly the same time, in the 9th week.

Finally, let us consider a last epidemiological peak.

![Pic3](https://user-images.githubusercontent.com/85577140/126783935-2ad71d0f-aaf2-4dd7-9609-acc0c0ff5b6a.jpg)
![Pic3MMC](https://user-images.githubusercontent.com/85577140/126784300-86ca3408-3132-46d8-815d-2c4e345f54a4.jpg)

This time the curve representing the real data had a rather peculiar shape differing from the usual bell shapes: exponential growth and then a rather smooth and flatter decay. Before applying the least squares method, it was clear that our model did not correspond well to reality. Indeed, although the growth of the two curves is similar at the beginning, the rate of infection reached at the peak of the epidemic for our model is almost double the rate from the real data.
The least squares method allowed us to reduce such a difference, but as can be seen on the last graph, the epidemic peak is not reached at the same time and arrives faster (at the 7th versus the 9th week) when considering the real data, which can be fatal when relying on this model to predict the evolution of the epidemic.


# 5 Discussion
## 5.1 Advantages and disadvantages of the SIR model

As we have seen, the SIR model does not take into account all the parameters, but already gives a first idea of how to model an epidemic peak. It is a fairly simple model, but it requires certain data to be found, such as the population, the infection rate and the cure rate. However, the choice of the value of these parameters is often more or less arbitrary, as is the choice of a fixed total population, which is in fact not the case. Furthermore, it should be noted that as this is a seasonal disease, the variants are not the same from one year to the next, thus modifying the different parameters.
Another important point to note about the SIR model is that it does not take into account certain aspects such as immunity acquired through exposure to the virus or through vaccination as well as non-infectious infected persons as the SEIR model can do. However, to be able to use these data effectively, more resources are needed on this subject and we have found that it is difficult to find stable information.

## 5.2 Advantages and disadvantages of least squares method

The principle of the least squares method is to compare whether our modelling is close enough to reality. The value obtained with the Solver tool in Excel is however only indicative and specific to this study (depending very particularly on the scale used). The advantage of this method is that we can find the values of the parameters that we can vary (in this case β and γ) in order to get closer to the real values.

SECTION A COMPLETER !! (voir résultats)
Nous a aidé à comprendre première technique de regression avec la méthode des moindres carrés, une méthode de régression parmi d'autres + mesurer de l'importance de la sensibilité du modèle etc
n'a pas vocation prédictive
différence de valeur entre les beta et gamma s'expliquent parle caractère saisonnier du virus + fortes proba de muta donc caractéristiques différentes etc.

# 6 Conclusion

This study allowed us to familiarise ourselves with the tools used in the case of epidemiological studies by means of simple tools. The search for reliable data led to the choice of the SIR model, as some data were inaccessible and a model that was too complex could not have been considered. Moreover, it would have required extensive knowledge of this field and a consequent number of parameters to manage. However, this model was able to model the selected epidemic peaks relatively closely. This model based on differential equations gives the first keys on how to formulate a problem from a mathematical point of view and how to interpret it correctly.
In the context of a health crisis related to COVID-19, it is this type of modelling that serves as a decision support tool for governments and public health authorities. Analyses and interpretations of these models must be done with parsimony since a model does not fully reflect reality and only represents probabilities of events at a given time and there will often be discrepancies between model results and actual observations that are inherent in the structure of the model itself and uncertainty about certain parameters. 


# References

Brauer F. (2008) Compartmental Models in Epidemiology. In: Brauer F., van den Driessche P., Wu J. (eds) Mathematical Epidemiology. Lecture Notes in Mathematics, vol 1945. Springer, Berlin, Heidelberg

Kermack, W. O. and McKendrick, A. G. (1927). Contributions to the mathematical theory of epidemics, part i. Proceedings of the Royal Society of Edinburgh. Section A. Mathematics. 115, 700-721.

Siettos, C. I., & Russo, L. (2013). Mathematical modeling of infectious disease dynamics. Virulence, 4(4), 295-306

Sentinelles, R. I. (2021). Données syndromes grippaux Réseau Sentinelles. Réseau Sentinelles. http://www.sentiweb.fr/france/fr/?page=table

Modélisation d'une épidémie - Images des mathématiques. (2020, novembre). CNRS. https://images.math.cnrs.fr/Modelisation-d-une-epidemie-partie-2.html\


### Supporting information
This paper is also written in LaTeX and in French, to get it, please reach me out. In the rest of this repo you will find the raw dataset. An illustrated appendix concerning the data cleaning set has also been written in French (but a bit heavy to import on GitHub). If you wish to read it, please do not hesitate to reach me out again.




