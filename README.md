# NBA-Champion-Predictor-Project

In this project, I used each (active) team's per-game stats (PTS, REB, AST, TOV) as well as their advanced stats in each season from 1996 to 2022 to predict who would be the NBA Champion that season. 

## **Summary**
The full predictions of the most likely NBA champion per season is in the PREDICTIONS folder. See predictions_2023_NBA_champion.csv for predictions of the 2023 NBA Season and see predictions_1996_2022_NBA_champion_ridge.csv for the predictions fro the 1996 - 2022 NBA Seasons.

In the above files, the higher the Predicted_Score, the more likely the team is to win the NBA champion. See **Cleaning and Parsing the Data** below for how each team's playoff score was determined for that season. 

In short, NBA Champion received 10 points, Runner-Up received 7 points, teams that lost in the Conference Finals received 4 points, teams that lost in the Conference Finals received 4 points, teams that lost in the Conference Semi-finals received 2 points, teams that lost in the First Round received 1 point and teams that didn't make the playoffs at all received no points.

## **Web Scraping**

I first web-scraped the per-game and advanced stats using WebDriver from Python's Selenium Library and those files are in the _**PER_GAME_STATS**_ and _**ADVANCED_STATS**_ folders respectively. <br><br> To quantify how well each team ended up performing in the playoffs (whether they won the Championship / Lost in the Finals / Missed the Playoffs Entirely) which is the dependent variable that the model will be trained on, I web-scraped a playoff bracket and this data can be found in the _**PLAYOFFS_DATA**_ folder.

## **Cleaning and Parsing the Data**

Next, I used Python's BeautifulSoup library and its classes and methods to parse and extract the necessary tables and delete any unnecessary information for the per-game stats, advanced stats and playoff table. <br>

Then, I used Python's Pandas library to clean the data (i.e. make sure I included only the relevant columns of data in my Dataframes, set any null values to 0, make sure each Team's name was the same historically, etc.). The most difficult part of this process was determining how to manage the playoff results data (i.e. where each team finished).<br>

I used a scoring system (playoff score) to quantify each team's playoff performance: <br> 

NBA Champion got **10** points<br>
Runner-Up got **7** points<br>
Conference Finals losers got **4** points<br>
Conference Semi-finals losers got **2** points<br>
First Round losers got **1** point<br>
Teams that didn't make the playoffs got **0** points.

I then merged all the DataFrames of each into one Dataframe and then exported it in the CSV file titled **_merged_stats_scores_**

## **Training the Model**

Finally, I used a Ridge Regression Model from Python's Scikit-Learn library to train the data on. Reason being:

It has an alpha value that tries to prevent overfitting of the data by adding a penalty function to the calculation of the Residual Sum of Squares (which is what we want to minimize since the lower the difference between the model's predictions and the actual data, the better). This way the model is more realistic and doesn't only work on the training data. 

This also reduces issues from highly correlated independent variables (multicollinearity).

## **BackTesting**

I employed a backtesting function to use all the previous seasons (at least 2 previous seasons) as the training dataset for the next season. This way, I tested on all years 1998-2022 and obtained the predicted results. 

## **Cross Validation**

To determine the best alpha value (which is the factor that determines how much regularization or penalty should be introduced) I used a 10-fold cross-validation function which split the data up 10 into 10 folds where each fold would be used once as the testing dataset.
This was run for each alpha value in the range of 10<sup>-9</sup> to 10<sup>9</sup>, increasing by a multiplicity factor of 10.

The alpha value that corresponded with the lowest mean squared error (the lower, the better) was chosen. Mean squared error is the average squared difference between the predicted values and the actual values.

## **Making the Predictions**

The final predictions are then saved in the CSV files called **_results_ridge_** and which contains all the predictions from 1998 to 2022. I included actual/predicted rankings to better indicate which team was the most likely to win the NBA Champion. 

The teams with the predicted ranking of 1 meant most likely, 2 is second most likely and so on. 

Since it was around the start of the NBA Finals, I also trained the model on the seasons from 1996 to 2022 on each team's 2023 per game and advanced stats data and it found that the two most likely teams to win the 2023 NBA Championship was the **_Boston Celtics_** and the **_Denver Nuggets_**, the latter of which actually won, so yay!

## **Files Where Each Step of the Project can be Found**
Code for web scraping and cleaning/parsing the per-game stats can be found in the **_scrape_clean_per_game_stats.ipynb_** file.<br>
Code for web scraping the advanced stats is in the _**web_scrape_advanced_stats.ipynb**_ file.<br>
Code for cleaning and parsing the advanced stats data is in the **_clean_adv_stats.ipynb_**.<br>
Code for web scraping the playoff scores is in the **_web_scrape_playoff.ipynb_**<br>
Code for cleaning and parsing the playoff scores is in the **_clean_playoff_data.ipynb_**<br>
Code for merging the per game stats, advanced stats and playoff scores **_merging.ipynb_**<br>
Code for the ridge regression model, backtesting and cross validation are found in _**ridge_regression.ipynb**_.

Code for the 2023 per game stats and advanced stats are found in the folder called _**2023_Predictions**_

# Thanks for Reading!
