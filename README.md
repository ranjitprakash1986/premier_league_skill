# Did Manchester United over-achieve in EPL 2022/2023  

* Author: Ranjit Sundaramurthi
* Attribution: [UBC-MDS DSCI 553](https://pages.github.ubc.ca/MDS-2022-23/DSCI_553_stat-inf-2_students/README.html)



After a poor start to the season with defeats against Brighton and Brentford in their opening two games of the Premier League 2022/2023 season, Manchester United seemed to be continuing their previous forgetful season form. The previous season they had finished 6th in the League and failed to qualify for the UEFA competition. With a 2021/2022 season with 58 points (their lowest tally), 56 conceded goals (their most conceded) and 16 wins (their fewest tally), things could only be expected to improve. However, the shaky start aggravated by the power battle between the new manager - Erik Ten Hag (ETH) and the talisman - Cristiano Ronaldo. ETH is often regarded as the next influential manager who can not only compete with the likes of Pep Guardiola and Jürgen Klopp, but also provide dynamic attacking football, a trait long associated with Manchester United. Those who follow EPL closely will agree the 2022/2023 season turned out to be roller coaster of a ride for Manchester United. With the ebbs and flows, Manchester United finished the season strongly  in third place and won the Carabao Cup trophy, their first trophy since 2016/2017 season.


In this article I assess the performance of Manchester United with their attack/defence polarity in comparison to the other league teams. In my analysis the intangible attacking intent, hereafter referenced as `skill`, is represented by using two approaches using Bayesian statistical analysis. 
   * The first one uses the score difference as an indicator of the skill (attack/defence polarity) of the two participating teams. For instance if a league game result is 1-2 or 4-0, the score difference is 1 and 4 respectively for these games. The score difference is a computed as a positive number and is modeled to be a reflection of the disparity in skill levels of the participating teams.
   * The second one uses the expected goal difference as the indicator of the skill (attack/defence polarity) of the two participating teams. You can understand more about expected goals [here](https://theanalyst.com/na/2021/07/what-are-expected-goals-xg/). In short, as the name indicates expected goals is a metric that reflects the attacking intent of a team by capturing the context of the gameplay. It can be much different than the number of actual goals scored by a team depending on the turn of events during the game.
   
   You can find the details on the modeling procedure [here](src/code.Rmd). I will limit this article to the overall discussion peppering it with technical details as necessary for support. The code is adapted from the lab assignment from [DSCI-553](https://pages.github.ubc.ca/MDS-2022-23/DSCI_553_stat-inf-2_students/README.html) of MDS program at UBC.


In the first approach the score difference is a positive non-zero integer. The drawn games are eliminated from consideration. The mean value of the score difference is given by $\lambda$ since it is assumed to be Poisson distributed. Thus a higher score_diff implies a higher value of $\lambda$, which in turn implies a higher difference in the skill levels of the winning and losing team for that game. I create a functional representation of $\lambda$ such that it increases with the increase in difference in the skill levels of the winning and the losing team. Consequently the expected score difference also increases. This makes sense in the the context of the modelling of a football game outcome. One model that meet this criteria is as follows. This is be the Likelihood function.

$$\lambda_i = \log\big(1 + \exp(w_i - l_i)\big)$$


I ran a R STAN simulation over 18,000 effective iterations drawing 900 iteration samples at intervals of 20 simulations. Each drawn simulated sample represents the skill level of each of the teams in the league based on the posterior distribution of lambda based on the evidence, i.e. actual score difference observed during the 2022/2023 league games. The fascination of Bayesian simulations is their tendency to converge to the true distribution with sufficient iterations. Please note that the quality of the simulations is pending to be tested. As of now, I will make inferences based on the simulation results.   


### Data


The data is sourced specifically from [fbref](https://fbref.com/en/comps/9/schedule/Premier-League-Scores-and-Fixtures) which provides the results for every game played during the 2022/2023 season. The data was cleaned using R to design in the required format for further analysis. The cleaned dataset is found [here](data/epl_2022_2023_matches.csv). Thanks to [Fbref](https://fbref.com/en/) for providing up to date statistics that enables us derive interesting and rewarding insights.

```python

```
