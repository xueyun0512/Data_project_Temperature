# Python - Temperature analysis 2023

## Introduction
In this second project, I worked with Python in order to analyse the temperature evolution of 2023 for all the districts in France.  <br> 
The Jupyter Notebook I wrote could be found in the same folder.

## Skills demonstrated
- Python - **panda**  and **matplotlib** libraries
- SQL - Window function (LAG) 

## Table of content 
1) Input data
2) Evolution of the minimum, maximum and average temperatures of the district Pays de la Loire 
3) Comparison of the monthly temperature changing regarding the district
4) How is the temperature increasing?
5) Conclusion

## 1) Input data 
The data comes from [here](https://odre.opendatasoft.com/explore/dataset/temperature-quotidienne-regionale/information/?disjunctive.region) and show the daily temperature (in °C) of 2023 in different districts in France. There are 3 types categories of temperature: the maximum _(Tmax)_, the minimum _(Tmin)_, and the average _(Tavg)_. <br>I've created an additional column _Temperature difference_ in order to visualize how the temperature increases. 

## 2) Evolution of the minimum, maximum and average temperatures of the district Pays de la Loire
Given the dataset, it may be interesting to plot and look at the difference between the minimum, the maximum and the average temperature. I was especially curious about the district of Pays de la Loire so I only plotted from it. I got the figure below: 

<p align="center">
  <img src="/Python_analysis/plots/loire_2023_python.png" width="600"/>
</p>

As it could be seen, the temperature experienced the biggest variation during summer. Indeed, it is really hot in summer and there is a big gap between the cold at night and the heatwave through the day. 

## 3) Comparison of the monthly temperature changing regarding the district
In this section, I've compared the monthly temeprature evolution in every district. Among the 12 months observed, there are the months of January, March, July and November that are more worth discussing. 

<p align="center">
  <img src="/Python_analysis/plots/January_2023_python.png" width="800"/>
</p>

One can notice that the temeprature profil isn't the same for every district in this cold month of Winter! While most of the districts follow the same temperature trend, _Corse_ does not obey to the rule and has the highest temeprature (around 12°C). This is not even surprising as _Corse_ is located in the South coast in France. One of the chillest place where to have holidays! 

Now, let's have a look on the month of March: 

<p align="center">
  <img src="/Python_analysis/plots/March_2023_python.png" width="800"/>
</p>

The temperature is increasing slowly as Spring is coming. It reaches around 15°C at the end of the month. Apart from the districts of _Corse, Nouvelle Acquitaine and Côte d'azur_ (located in the South for the three of them), the temperature evolution is nearly the same for all districts.

Evry district does not experience the same temperature model in July. There is a dispatching. Depending of the location, the temperature could be really different. For instance, _Corse_ (once again) has recorded the highest temperature (lore than 30°C) while _Bretagne_, in the North-West has experienced the lowest temperature (around 18°C).

<p align="center">
  <img src="/Python_analysis/plots/July_2023_python.png" width="800"/>
</p>

Through the month of November, the country is welcoming Winter and the temperature is noticeably decreasing: from 12.5°C to 2.5 °C. Except _Corse_ that only shuts down from 17.5°C to 12.5°C and is still hotter in comparison with other districts.
Winter is coming and poeple should be careful about the brute temperature variation. 
<p align="center">
  <img src="/Python_analysis/plots/November_2023_python.png" width="800"/>
</p>

## 4) How is the temperature increasing?
As we are given the daily temperature, it could be fun to study how the temeprature changes. This can be really helpful in order to know when people have to be cautious about a sudden temperature variation. I defined the temperature rate as: $\delta T = T_{day,d+1}-T_{day,d}$. <br>
First, I defined a column _Prev_temperature_ using the function **_LAG_** in SQL. Then, I added a second column as _Prev_temperature - Tavg_. 

The folliwing picture show the temperature variation rate for the districts of Corse and Bretagne. One can mitice that in Bretagne, the temperature can increase or decrease dratiscally from a day to the next: the variation could reach 6°C. As Bretagne has one of the coldest weather in France, this resultat is not surprising. <br> The temeprature variation rate in Corse is a bit lower than the previous district. The maximum variation is less than 5°C. 
Therefore, no matter if the weather is cold or not, the temperature variation rate is in the same range.

<p align="center">
  <img src="/Python_analysis/plots/corse_bretagne_python.png" width="800"/>
</p>

<h1 align="center">Bretagne</h1>
![](/Python_analysis/plots/['Bretagne']_python.png)

<h1 align="center">Corse</h1>
![](/Python_analysis/plots/['Corse']_python.png)

## 5) Conclusion
This temperature analysis shows us how is the temeprature evolution in several French districts. Some areas are facing high temperature constantly during the year (eg Corse) while other districts does not (eg Bretagne). However, the temeprature variation rate from day D to day D+1 is approximately the same for every district, around 5°C. <br>
Through this project, I have learnt how to use Python librairies (_pandas_ and _matplotlib_ especially) for Data analysis. 
