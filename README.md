# NBA-Champion-Predictor-Project

In this project, I used each (active) team's per-game stats (PTS, REB, AST, TOV) as well as their advanced stats in each season from 1996 to 2022 to predict who would be the NBA Champion that season. 

## **Web Scraping**

I first web-scraped the per-game and advanced stats using WebDriver from Python's Selenium Library and those files are in the DATA and ADVANCED folders respectively. <br><br> To quantify how well each team ended up performing in the playoffs (whether they won the Championship / Lost in the Finals / Missed the Playoffs Entirely) which is the dependent variable that the model will be trained on, I web-scraped a playoff bracket.

## **Where the Code can be Found**
Code for web scraping and cleaning/parsing the per-game stats can be found in the **_scrape_clean_per_game_stats.ipynb_** file.<br>
Code for web scraping the advanced stats is in the _**web_scrape_advanced_stats.ipynb**_ file.<br>
Code for cleaning and parsing the advanced stats data is in the **_clean_adv_stats.ipynb_**.<br>
Code for web scraping the playoff scores is in the **_web_scrape_playoff.ipynb_**<br>
Code for cleaning and parsing the playoff scores is in the **_clean_playoff_data.ipynb_**
