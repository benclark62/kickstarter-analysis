# Kickstarting with Excel

## Overview of Project
Louise, an aspiring play producer, conducted a Kickstarter campaign to fund her play, Fever.  Her initial campaign delivered less than the stated goal (86% of goal) and she has requested additional research to be conducted about comparable projects. 
I investigated trends in data retrieved from the Kickstarter website that allowed me to segment campaign performance in ways that were relevant to Louise’s approach.  This analysis will provide Louise with insights for making decisions around campaign timing and goal-setting, while identifying additional analysis that would inform future campaigns. 

### Purpose
As a consultant employed by Louise, my objective is to leverage data retrieved from Kickstarter to analyze comparable campaigns in order to provide informed recommendations for future campaigns.  This analysis ultimately centered on understanding the importance of timing and goal-setting when predicting the likelihood of a campaign’s success.

## Analysis and Challenges
Kickstarter data provided information for 4,115 distinct campaigns covering nine parent categories (i.e. Theater, Games, and Music) and 41 sub-categories (i.e. Plays, Drama, and Jazz) spanning eight years.  Key metrics included were:
-	Unique event identifiers (ID)
-	Campaign details:  names, descriptions, locations, and campaign duration
-	Campaign performance: Goals ($), Pledged ($), number of supporters, 
Analysis was conducted to understand performance trends that could inform future campaign decisions.   

### Analysis of Outcomes Based on Launch Date
“Successful” campaign was one in which the amount raised (“pledged”) met or exceeded the amount intended to be raised (“goal”) while “failed” campaigns were those which did not achieve that standard. 
Defining the launch date required converting timing information from Unix timestamps into more easily discernable, traditional date format (MM/DD/YYYY).  In order to make this conversion, the formula below was used to convert to total seconds elapsed between the Epoch Date (January 1st, 1970) used in Unix timestamps into a traditional date format.
=(((J2/60)/60)/24)+DATE(1970,1,1)
With the data formatted correctly, a Pivot table was created to sort campaign outcomes by their launch date.  In my version of Excel, the data was automatically formatted into Years and Quarters.  This required an additional step of “ungrouping” the Row Labels into more granular monthly data.  With the Pivot table formatted to show outcomes (Successful, Failed, Canceled) by month, I added a Pivot Chart to visualize the data.

![Outcomes_vs_Goals.png](https://github.com/benclark62/kickstarter-analysis/blob/main/resources/Outcomes_vs_Goals.png)

With the data presented in a line chart, it became apparent that the months with the greatest absolute number of successful theater campaigns were May, June, and July.  These months averaged 99.3 successful campaigns per month compared to an average of 60.1 successful campaigns for the remainder of the year.  In addition to the highest absolute number of successful campaigns, the months of May, June, and July also had the highest success rate (Successful campaigns / total campaigns) during the year, indicating that this would be the best time to launch a theater campaign.

### Analysis of Outcomes Based on Goals
Goals for theater projects, or the targeted amount of funds to be raised by a Kickstarter campaign, ranged from one dollar to $30,000,000, though 84.9% were for less than $9,999.  In order to better understand the relationship between goal size and campaign outcomes, the data needed to be formatted in a manner that makes it clear to see patterns by goal size.
Using simple break points, a table was created to categorize the goals by size and to illustrate the corresponding outcomes.  The COUNTIFS() function in Excel was used to count the number of campaigns that fell into each goal grouping.  The formula below illustrates the formula used to count the number of successful campaigns whose goals were greater than or equal to $1,000 and less than or equal to $4,999. 
=COUNTIFS(Kickstarter!$D:$D,">=1000",Kickstarter!$D:$D,"<=4999",Kickstarter!$F:$F,"successful",Kickstarter!$R:$R,"plays")
With the counts of campaign outcomes assigned to goal size groupings, we now calculated the outcome rates (i.e. count of successful / count of total for goal size grouping) to determine the goal sizes that produced the highest rates of successful campaigns

![Theater_Outcomes_vs_Launch.png](https://github.com/benclark62/kickstarter-analysis/blob/main/resources/Theater_Outcomes_vs_Launch.png)

Converting the outcome rate data into a line chart made it clear that the goal size groupings with the highest likelihoods for success were those less than $15,000.  Campaigns with goals between $35,000 and $44,999 demonstrated higher success rates, but this appears to be an anomaly based on a small sample size (only 9 campaigns, or 0.8% of theater campaigns fell into that range).

### Challenges and Difficulties Encountered
The data was presented in an easy-to-understand format with minimal data cleansing required prior to conducting the analysis.  Had we been asked to conduct deeper analysis across different countries, applying conversion rates to different currencies would have been necessary and potentially difficult in order to provide realistic comparisons.

## Results

### - What are two conclusions you can draw about the Outcomes based on Launch Date?
First, for theater campaigns, the highest number of successful campaigns and the highest success rates occur in the early summer months of May, June, and July.  Second, these months also are among the four highest months in absolute number of failed campaigns, implying that there could be increased competition for finite contributions.

### - What can you conclude about the Outcomes based on Goals?
Campaigns with goals under $14,999 have the highest success rates of all theater campaigns.  The one exception would be campaigns between $35,000 and $44,999, but these had very small volume of campaigns (0.8% of all theater campaigns).  The smaller goals are obviously easier to achieve, but this could also imply that larger theater projects would be more successful seeking funding through channels other than Kickstarter.

### - What are some limitations of this dataset?
The success of a Kickstarter campaign relies on many factors beyond goal size and timing, many of which are qualitative (e.g. how compelling is the story or sales pitch) and additional information that would be difficult to easily compile (e.g. how did the campaign owner market their campaign).
There is geographic variability that would influence a campaigns success that can not be determined at the national level.  For example, a theater Kickstarter campaign in New York may not succeed as quickly as one in Topeka due to different levels of competition or costs required to accomplish a similar theater execution. 

### - What are some other possible tables and/or graphs that we could create?
I would visualize the data at a more granular level that would be more relevant for Louise’s decision-making process.  For example, more relevant insights could be gained by developing a similar launch dates line chart but looking only at weekly results for campaigns for plays that were launched in the U.S. in 2016.
Louise’s campaign had a very high average donation (331% of the average theater donation), so I would illustrate her campaign performance to others with comparable average donations.  That information would convey that her campaign – while not technically successful – could study other similar campaigns and have more success in subsequent rounds of fundraising. 
