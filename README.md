
# IPL Match-Dashboard

## Problem Statement

To create an interactive and comprehensive dashboard in Power BI for analyzing Indian Premier League (IPL) matches. The dashboard will provide insights into match outcomes, player performances, team statistics, and other key metrics to facilitate data-driven decision-making and enhance fan engagement.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 :Check datatype of all columns, then go to home tab  and close and apply.
- Step 5 : Add canvas background and add title for the dashboard as "IPL Analysis".
- Step 6 : Create calender table for data visualization using DAX function.
             
       Calendar Table = CALENDAR(MIN(ipl_matches_2008_2022[match_date]),MAX(ipl_matches_2008_2022[match_date]))

- Step 7 : Visual filters (Slicers) was added for field named "Year" and "Year" column was added in calender table using DAX function.
         
          Year = YEAR('Calendar Table'[Date])

  ![Screenshot 2024-07-02 171324](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/93142a58-e96b-4554-8e3a-3f88f6d0cec7)
- Step 8 : Five card visuals(KPI) were added to the canvas,representing title winner, orange cap holder, purple cap holder,tournament's 6 and tournament's 4 with some filtering.

![Screenshot 2024-07-03 112111](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/cf70489b-2195-4199-a831-6b36ca44968b)
      
Following DAX functions were used to show above KPI's

        * Title Winner
          Title Winner = VAR max_date=CALCULATE(MAX('Calendar Table'[Date]),ALLSELECTED(ipl_matches_2008_2022),VALUES(ipl_matches_2008_2022))
            var Title_winner = CALCULATE(SELECTEDVALUE(ipl_matches_2008_2022[winning_team]),'Calendar Table'[Date]=max_date)
            RETURN Title_winner

        * Orange Cap
            Batter Runs = CONCATENATE(SUM(ipl_ball_by_ball_2008_2022[batsman_run])," Runs")

         * Purple Cap
            Bowler Wickets = CONCATENATE(SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery])," Wickets")

- Step 9 : To show IPL batting statistics, card visuals were used to represent batsman, total runs, sixes ,four and strike rate and DAX functions and filtering were used.

   ![Screenshot 2024-07-03 125118](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/362eb3e9-7f76-4c17-a8f9-53004858417e)

Following DAX function was used to calculate strike rate

        * Strike Rate
            Strike Rate = (sum(ipl_ball_by_ball_2008_2022[batsman_run])/count(ipl_ball_by_ball_2008_2022[ball_number]))*100

- Step 10 : To show IPL bowling statistics, card visuals were used to represent wickets, economy,average rate and bowling strike rate and DAX functions and filtering were used.

   ![Screenshot 2024-07-03 151228](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/a06b97b2-6b8a-4083-b8e5-50416a699d92)

Following DAX functions was used to calculate economy, average rate, bowling strike rate.

        * Economy
            Economy = DIVIDE(SUMX(FILTER(ipl_ball_by_ball_2008_2022,ipl_ball_by_ball_2008_2022[extra_type]<>"legbyes" && ipl_ball_by_ball_2008_2022[extra_type] <> "byes"),
            ipl_ball_by_ball_2008_2022[total_run]),COUNT(ipl_ball_by_ball_2008_2022[overs])/6)

        * Average Rate
            Average Rate = DIVIDE(SUMX(FILTER(ipl_ball_by_ball_2008_2022,ipl_ball_by_ball_2008_2022[extra_type]<>"legbyes" && ipl_ball_by_ball_2008_2022[extra_type] <> "byes"),
            ipl_ball_by_ball_2008_2022[total_run]),sum(ipl_ball_by_ball_2008_2022[iswicket_delivery]))

        * Average Rate
            Bowling SR = COUNT(ipl_ball_by_ball_2008_2022[bowler])/SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery])

- Step 11 : To show matchs win by result type like won by wickets, runs,superover pie chart was used.

![Screenshot 2024-07-03 160742](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/d817d77b-db70-4bd4-9c73-0b911b6076d1)

- Step 12 : To show winning percentage on toss decision pie chart was used but directly data not avilable so use DAX function.

      Matches win on toss decision = CALCULATE(COUNTROWS(ipl_matches_2008_2022),ipl_matches_2008_2022[toss_winner]=ipl_matches_2008_2022[winning_team])

![Screenshot 2024-07-03 160731](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/b81da07b-dffe-4582-bbc9-4a92bd2f2e4c)

- Step 13 : To show total win by team bar chart was used.

![Screenshot 2024-07-03 160707](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/a45057c4-4410-46ee-b249-0ba2e47780a9)

- Step 14 : To show matches win in top 5 venue bar chart was used and top N filter was applied.

![Screenshot 2024-07-03 162601](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/fff89343-8160-48be-932b-8cc089bd2f93)

 - Step 15 : The report was then published to Power BI Service.
 
 # Report Snapshot (Power BI DESKTOP)

 
![Screenshot 2024-07-03 163012](https://github.com/Smitamane25/Ecommerce-Sales-Dashboard/assets/171058471/1a122373-cdb9-4909-a40a-e55c4926307c)

# Insights


### [1] Team Performance

   Teams like Mumbai Indians (MI) and Chennai Super Kings (CSK) have shown consistent performance, frequently reaching playoffs and winning multiple titles.


### [2]  Winning Strategies
Winning the toss and choose field has often been a successful strategy.

        Toss decision and Matches win
        Field = 330 matches (67%)
        Bat = 159 matches (33%)

### [3] Player Performance Insights
Top Run Scorers: Players like Virat Kohli, Suresh Raina, and Rohit Sharma consistently rank among the top run-scorers.

Leading Wicket-Takers: Bowlers such as  DJ Bravo, and Yuzvendra Chahal have been leading wicket-takers, showcasing their impact on the game.
