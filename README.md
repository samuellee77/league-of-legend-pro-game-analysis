**Names**: Samuel Lee, Nian-Cin Wang

## Introduction

The data set we are working with is professional League of Legends match data for 2022. The main question we explore throughout this EDA is what makes a team win a match. We mainly look at two aspects: the team's side (blue or red) and the champions they have selected and banned. One of the original motivations for this is due to the widely known rumor that the blue side wins more than the red, and teams tend to choose to be on the blue side when they have priority. We want to verify whether the rumor is true and back it up with data. On the other hand, we are also curious how much of an impact the champions being selected or banned have on the outcome of the match.

Our data set is accessed from the website Oracle’s Elixir: https://oracleselixir.com/tools/downloads. The original data consists of 148992 rows. Every 12 rows is data for a single match; 10 of them are player data, and 2 are team data. In our project, we have decided to focus on Tier 1 and split the data into two sets: player data and team data.

The main columns we work with are `gameid`, `url`, `league`, `split`, `playoffs`, `patch`, `side`, `ban1`, `ban2`, `ban3`, `ban4`, `ban5`, `pick1`, `pick2`, `pick3`, `pick4`, `pick5`, `gamelength`, `result`. Among all, `side`, `ban1`, `ban2`, `ban3`, `ban4`, `ban5`, `pick1`, `pick2`, `pick3`, `pick4`, `pick5`, `result` were mainly used for exploring the factors for the team to win. Most others were used for early exploratory data analysis and data cleaning to understand more about the data set.

The description to the relevant columns are as follows:
- `gameid`: unique player identification number
- `url`: url to game data else NaN
- `league`: team name
- `split`: 
- `playoffs`: 
- `patch`: version of game
- `side`: the teams side, either red or blue
- `ban1`, `ban2`, `ban3`, `ban4`, `ban5`: the 5 champions banned by the opposing team, meaning the champions that cannot be used
- `pick1`, `pick2`, `pick3`, `pick4`, `pick5`: the 5 champions being picked by the team
- `gamelength`: time the game took in seconds
- `result`: 1 if the team won or otherwise

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

For the data cleaning, we first separate the orignal dataset into two: `tier1_player` and `tier1_team` because we found that the rows in the original dataset belong to two categories of players and teams. If we don't separate them, there will be many missing by design values. 

### Univariate Analysis

#### Number of Games Played in Each Patch

We can see that there were no games played in tier 1 leagues in 12.07, and there were only few games in 12.06, 12.08, and 12.16. It is because that most league spring playoffs happened in 12.05 and 12.06, so there was no game played in 12.07. The Mid-Seasonal Invitational(MSI) was hold during 12.08, so there was few games in 12.08 in tier 1 leagues, as we do not include the international competitions. Same reason apply to 12.16, most league summer playoffs happened in 12.15 and 12.16, and then the Worlds happened in 12.18.

<iframe
  src="assets/fig1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Distribution of Game Length

For the following plot, we can see that the distribution of game length is skewed to the right, with the **median** of **31.39 minutes**.

<iframe
  src="assets/fig2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

#### Average Game Length in Each Tier 1 League
From the following boxplot and barplot, we can see that there is no significant game length between each league. One interesting fact is that **LCK**, known for best game strategy in the game with less teamfight, has the longest average game length, while **VCS**, known for its bloody and frequent teamfights, has the shortest average game length.

<iframe
  src="assets/fig3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/fig4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Blue / Red Team Win Rate in Each Tier 1 League

From the table and grouped barplot below, we can see that in most leagues (except LCS, LLA, and VCS), **the win rate of blue side is higher than the win rate of red side.** Especially in PCS, the difference of the win rates between blue and red sides is about 0.20, which is a significant amount that can affect the result of the game.

| league   |     Blue |      Red |
|:---------|---------:|---------:|
| CBLOL    | 0.539095 | 0.460905 |
| LCK      | 0.507495 | 0.492505 |
| LCO      | 0.514151 | 0.485849 |
| LCS      | 0.493464 | 0.506536 |
| LEC      | 0.534979 | 0.465021 |
| LJL      | 0.514019 | 0.485981 |
| LLA      | 0.491979 | 0.508021 |
| LPL      | 0.549618 | 0.450382 |
| PCS      | 0.605166 | 0.394834 |
| VCS      | 0.495356 | 0.504644 |

<iframe
  src="assets/fig5.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates

#### Number of Games Played in Each Tier 1 League in 2022

From the plot below, we can see that LPL has the most games played in 2022. This is because they had 17 teams with Single Round Robin and BO3(Best of three) in regular seasons. [(Source)](https://lol.fandom.com/wiki/LPL/2022_Season) The second largest is LCK, which had 10 teams with Double Round Robin and BO3 in regular seasons. [(Source)](https://lol.fandom.com/wiki/LCK/2022_Season)

<iframe
  src="assets/fig6.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Most Picked Champions in Each Position
We first create a pivot table to count the times of champions picked in the roles.

| champion   |   Top |   Jungle |   Mid |   Bot |   Support |
|:-----------|------:|---------:|------:|------:|----------:|
| Aatrox     |   224 |        0 |     1 |     0 |         0 |
| Ahri       |     0 |        0 |   886 |     0 |         0 |
| Akali      |   144 |        0 |   203 |     0 |         0 |
| Akshan     |    21 |        0 |     2 |     0 |         0 |
| Alistar    |     0 |        0 |     0 |     0 |       270 |

From the plots below, we can see the most played 10 picked champions in each position.
<iframe
  src="assets/fig7-1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig7-2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig7-3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig7-4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig7-5.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Assessment of Missingness
### NMAR Analysis
NMAR occurs when the probability of data being missing depends on unobserved information. As we focus on data for tier 1, we realize that `url` column in the dataset is missing for some rows. We see how the LPL is not missing any urls, while others teams completely do not have any urls or have some. If LPL consistently provides this URL while other teams vary, it suggests that the missingness is related to the specific teams themselves. This is NMAR because the presence or absence of a URL linking to match information depends on the team; however, it cannot be recovered by other columns.

This indicate differences in how teams handle data reporting regarding match information. It could also reflect differences in resources, priorities, or organizational policies among the teams.

### Missingness Dependency	
We would like to carry out permutation tests to test if the missingness of  `ban1` to `ban5` columns are dependent to the `side` column. We chose the test statistic of **TVD** and the p-value cutoff of **0.05**.

<iframe
  src="assets/fig8-1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig8-2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig8-3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig8-4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig8-5.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

From the graph above, we can see that the p-values of the permutation tests for 5 ban columns are **much larger than 0.05**, which means that the missingness in the ban columns are **not dependent** on the side of the team.

However, is the missingness of ban1 column related to missingness of ban2, ban3, ban4, and/or ban 5? We can perform another permutation test to answer this question.

<iframe
  src="assets/fig9-1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig9-2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig9-3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig9-4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Therefore, from the above plots, it is clear that the missingness of `ban1` is related to the missingness of other `ban` columns.

## Hypothesis Testing

- Null hypothesis: The win rates of teams on the Blue and Red sides are equal.
- Alternative hypothesis: The win rate of teams on the Blue side is higher than the win rate of teams on the Red side.
- Test statistic: The difference in proportions of win games between the Blue and Red sides.
- Significant Level(p-value cutoff): 0.05
- We will perform permutation test to test the hypothesis.

The observed test statistic is 0.0553. The p-value is 0.0. Since the p-value is less than the significant level (0.05), we reject our null hypothesis. From our test, the win rate of teams on the Blue side is higher than the win rate of teams on the Red side.
<iframe
  src="assets/fig10.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Framing a Prediction Problem

Our prediction problem is that we want to predict the result of the game at the end of ban/pick. Therefore, it is a binary classification problem. We use the DecisionTreeClassifer to predict 0 and 1 for the `result` column. We use accuracy os our metric because we think that it gives us the most basic idea on our model's performance.

## Baseline Model

In the baseline model, we use `pick1` to `pick5` columns as features. They are all nominal variable, having the names of the champions, which is string, so we have 5 nominal features in our baseline model. We use customized one hot encoder to solve the problems that some champions may not appear in the train data but can appear in the test data. We used the `DecisionTreeClassifier` with the max depth of 5 to predict. 

Our train score is 0.5244, and our test score is 0.4756, which are very low, even lower than random chance (p = 0.50). Therefore, we need to include new features and change our feature engineering process.

## Final Model

For this part, we are going to include the `side` column as a new feature to predict the result of the game because we think that side selection can affect the result. As we demostrated earlier, the win rate of blue side is higher than the win rate of red side.

For feature engineering part, we would like to add the feature of pick rate of each champion because this can provide more information about the strength of individual champions. Therefore, we build another customized one hot transformer that one hot encode the champions and also include the pick rate of them.

The train and test scores of our new model now become 0.5564 and 0.5151. We can see that the accuracy improves a little bit. We are going to find the best hyperparameters for our model. After running through different hyperparameters, the best hyperparameters are the max_depth of 4 and the min_samples_split of 2, which has the test score of 0.5538.

The final model has a 0.05 higher accuracy than our baseline mode. Although it is not very high, we believe that those are reasonable because players and teams are more important than the champions they pick and the side they choose.

## Fairness Analysis

For conducting fairness analysis, we want to compare whether the model works equally for both blue and red side. As our hypothesis testing concluded that we cannot be sure if their side has an effect on winning, we want to further compare the performances between these two groups.

![img2](assets/img2.png)

With consideration that teams may consider selecting champions as one important factor to winning a match, cost of false positive of high. It is worse than false negative, where we predict them to lose while they actually won the match during the game. The grid above also shows out of 183 times, 76 teams actually lost when our model predicted them to win. Therefore, we decide to evalue our model's performance on **precision**, which is 0.5849.
