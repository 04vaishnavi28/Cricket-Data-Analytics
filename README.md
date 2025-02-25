# Best XI Selection from 2023 World Cup

## Project Overview

This project aims to identify and select the top 11 players from the 2023 World Cup who would make the best team. The selection is based on specific parameters tailored to form a balanced and competitive team. The final selection includes:

- **Openers**: 2 players
- **Anchors**: 3 players
- **Finisher**: 1 player
- **All-rounders**: 2 players
- **Fast bowlers**: 3 players

## Steps Followed

### 1. Parameter Selection for Victory
Identified key performance indicators (KPIs) crucial for team success in the World Cup. These parameters include batting averages, strike rates, bowling economy rates, and fielding statistics among others.

The team should meet the following criteria:
- **Average team score**: 180 runs or more.
- **Ability to defend**: 150 runs or more.

### Player Roles and Parameters

### 1. Openers

| Parameter         | Description                             | Criteria     |
| ----------------- | --------------------------------------- | ------------ |
| Batting Average   | Average runs scored in an innings        | > 30         |
| Strike Rate       | No. of runs scored per 100 balls         | > 120        |
| Innings Batted    | Total innings batted                     | > 3          |
| Boundary %        | % of runs scored in boundaries           | > 50%        |
| Batting Position  | Order in which the batter played         | < 7          |

### 2. Anchors / Middle Order

| Parameter         | Description                             | Criteria     |
| ----------------- | --------------------------------------- | ------------ |
| Batting Average   | Average runs scored in an innings        | > 40         |
| Strike Rate       | No. of runs scored per 100 balls         | > 105        |
| Innings Batted    | Total innings batted                     | > 3          |
| Avg. Balls Faced  | Average balls faced in an innings        | > 20         |
| Batting Position  | Order in which the batter played         | > 2          |

### 3. Finisher / Lower Order Anchor

| Parameter         | Description                             | Criteria     |
| ----------------- | --------------------------------------- | ------------ |
| Batting Average   | Average runs scored in an innings        | > 25         |
| Strike Rate       | No. of runs scored per 100 balls         | > 110        |
| Innings Batted    | Total innings batted                     | > 3          |
| Avg. Balls Faced  | Average balls faced in an innings        | > 12         |
| Batting Position  | Order in which the batter played         | > 3          |
| Innings Bowled    | Total innings bowled                     | > 1          |

### 4. All-Rounders / Lower Order

| Parameter         | Description                             | Criteria     |
| ----------------- | --------------------------------------- | ------------ |
| Batting Average   | Average runs scored in an innings        | > 15         |
| Strike Rate       | No. of runs scored per 100 balls         | > 110        |
| Innings Batted    | Total innings batted                     | > 1          |
| Batting Position  | Order in which the batter played         | > 2          |
| Innings Bowled    | Total innings bowled                     | > 1          |
| Bowling Economy   | Average runs allowed per over            | < 7          |
| Bowling Strike Rate| Average no. of balls to take a wicket   | < 50         |

### 5. Specialist Fast Bowlers

| Parameter         | Description                             | Criteria     |
| ----------------- | --------------------------------------- | ------------ |
| Innings Bowled    | Total innings bowled                     | > 1          |
| Bowling Economy   | Average runs allowed per over            | < 7          |
| Bowling Strike Rate| Average no. of balls to take a wicket   | < 16         |
| Bowling Style     | Bowling style of the player              | "%Fast%"     |
| Bowling Average   | No. of runs allowed per wicket           | < 20         |
| Dot Ball %        | % of dot balls bowled                   | > 40%        |

### 2. Data Collection
Gathered comprehensive data from all matches in the 2023 World Cup. The dataset includes player statistics, match outcomes, and other relevant performance metrics.
The dataset is downloaded from [ODI World Cup 2023](https://www.kaggle.com/datasets/enggbilalalikhan/odi-world-cup-2023-complete-dataset?select=odi+world+cup+2023+dataset)

### 3. Data Cleaning and Transformation
Processed the raw data to remove inconsistencies and inaccuracies. This step involved handling missing values, correcting data formats, and ensuring uniformity across the dataset.
[Jupyter Notebook](https://github.com/04vaishnavi28/Cricket-Data-Analytics/blob/main/Data%20Cleaning%20and%20Transformation.ipynb)

### 4. Data Transformation Using Power Query
Leveraged Power Query to transform the cleaned data into a more analyzable format. This step involved merging tables, creating calculated columns, and applying necessary data transformations to facilitate analysis.

### 5. Data Modeling and Building Parameters Using DAX
Used Data Analysis Expressions (DAX) to create sophisticated models and metrics. This involved calculating advanced performance metrics and modeling player contributions to team success.

#### Measures List

| Measure                  | Description                                                       | DAX Formula                                                                                                                      | Table                |
|--------------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|----------------------|
| Total Runs                | Total number of runs scored by the batsman                        | Total Runs = SUM(batting_summary[runs])                                                                                          | batting_summary      |
| Total Innings Batted      | Total number of innings a batsman got a chance to bat             | Total Innings Batted = COUNT(batting_summary[match_id])                                                                          | batting_summary      |
| Total Innings Dismissed   | To find the number of innings batsman got out                    | SUM(batting_summary[out])                                                                                                        | batting_summary      |
| Batting Average           | Average runs scored in an innings                                | Batting Avg = DIVIDE([Total Runs],[Total Innings Dismissed],0)                                                                   | batting_summary      |
| Total Balls Faced         | Total number of balls faced by the batsman                       | total balls faced = SUM(batting_summary[balls])                                                                                  | batting_summary      |
| Strike Rate               | No of runs scored per 100 balls                                  | Strike rate = DIVIDE([Total Runs],[total balls faced],0)*100                                                                     | batting_summary      |
| Batting Position          | Batting position of a player                                     | Batting Position = ROUNDUP(AVERAGE(batting_summary[batting_pos]),0)                                                              | batting_summary      |
| Boundary %                | Percentage of boundaries scored by the Batsman                   | Boundary % =  DIVIDE(SUM(batting_summary[Boundary runs]),[Total Runs],0)                                                         | batting_summary      |
| Avg. Balls Faced          | Average balls faced by the batter in an innings                  | AVERAGE(batting_summary[balls])                                                                                                  | batting_summary      |
| Wickets                   | Total number of wickets taken by a bowler                        | wickets = SUM(bowling_summary[wickets])                                                                                          | bowling_summary      |
| Balls Bowled              | Total number of balls bowled by the bowler                       | balls Bowled = SUM(bowling_summary[balls])                                                                                       | bowling_summary      |
| Runs Conceded             | Total runs conceded by the bowler                                | Runs Conceded = SUM(bowling_summary[runs])                                                                                       | bowling_summary      |
| Bowling Economy           | Average number of runs conceded in an over                       | Economy = DIVIDE( [Runs Conceded], ([balls Bowled]/6),0)                                                                         | bowling_summary      |
| Bowling Strike Rate       | Number of balls bowled per wicket                                | Bowling Strike Rate = DIVIDE([balls Bowled], [wickets],0)                                                                        | bowling_summary      |
| Bowling Average           | No. of runs allowed per wicket                                   | Bowling Average = DIVIDE([Runs Conceded],[wickets],0)                                                                            | bowling_summary      |
| Total Innings Bowled      | Total number of innings bowled by a bowler                       | Total Innings Bowled = DISTINCTCOUNT(bowling_summary[match_id])                                                                  | bowling_summary      |
| Dot Ball %                | Percentage of dot balls bowled by a bowler                       | Dot ball % = DIVIDE(SUM(bowling_summary[zeros]), SUM(bowling_summary[balls]),0)                                                  | bowling_summary      |
| Boundary Runs             | Total number of runs scored by hitting fours and sixes           | boundary runs = batting_summary[fours]*4 + batting_summary[sixes]*6                                                              | batting_summary      |
| Boundary Runs Bowling     | Total number of runs conceded by bowlers in boundaries           | Boundary runs = bowling_summary[fours]*4 + bowling_summary[Sixes]*6                                                              | bowling_summary      |
| Player Selection          | To understand if a player is selected or not                     | Player Selection = if(ISFILTERED(dim_player[name]),"1","0")                                                                      |   Others   |
| Display Text              | To display a text if no player is selected                       | Display Text = if([Player Selection] = "1", " " ,"Select Player(s) by clicking  the player’s name to see their individual strength.") | Others   |
| Color Callout Value       | To display a value only when a player is selected                | Color Callout Value = if([Player Selection]="0", "#F4F2DE", "#7C9D96")                                                            |   Others   |


### 6. Building Visuals and Dashboard
Developed a comprehensive dashboard to visualize the analysis. The dashboard includes various charts and tables that display player performance metrics and comparisons.

### 7. Selecting the Final 11
Based on the analysis, selected the top 11 players who fit the defined roles and parameters to form the best possible team.

## Dashboard Overview

### Page 1: Player Analysis
This page is divided into five sub-pages, each focusing on a specific player role. 
Each sub-page includes various visualizations such as tables, matrices, cards, line charts, and scatter charts to display player performance. Hovering over a player in the table reveals detailed performance statistics for each match.

1. **Openers**

![1](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/803560ed-eb32-41a9-a34d-307e08ed3210)
![2](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/7c4a1fd6-31d5-4c8a-b125-7e7c1d0eb03f)
![3](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/2881fbfc-8f05-46fb-9050-8b094a470572)

2. **Anchors**

![4](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/a18ade48-ba1d-410d-8ab1-6b81a4a016d7)
![5](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/86e1b805-9028-43db-af74-f5cf50922a74)
![6](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/86ce63c1-3674-437e-a3df-b2b8b6888180)

3. **Finishers**

![7](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/62a5eb06-2d48-4c72-b935-ba32d367fefc)
![8](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/45ba696f-ec32-456e-b4bc-7da314469290)
![9](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/0a740e12-a301-4924-bcfa-340bef094d32)

4. **All-rounders**

![10](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/ad681338-9e40-4005-b4ed-01128d1720ba)
![11](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/cb467fb3-fc89-4e7c-9da0-fae51c2986ba)
![12](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/498c78ef-84ab-4b8a-9a43-789c6e051ee8)

5. **Fast Bowlers**

![13](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/9d008392-dafd-447b-b113-f809a426df6c)
![14](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/16852512-7ea8-415a-95f6-af2fc0507015)
![15](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/d22e2d2c-9c8a-438b-89a7-7e9eb3c5e956)


### Page 2: Final 11
This page presents the selected final 11 players. It provides an overview of their key statistics and highlights why each player was chosen for their respective roles.

![16](https://github.com/04vaishnavi28/Cricket-Data-Analytics/assets/132866693/42b665ea-47f8-4f0b-8338-fe3199f36780)

## Conclusion
This project provides a data-driven approach to selecting the best XI from the 2023 World Cup. By utilizing advanced data analytics and visualization techniques, the project offers valuable insights into player performances and optimal team composition.


---

You can find the code and detailed documentation for this project in the repository. Your feedback and contributions are welcome!
