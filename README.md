# Olympics Games Analysis

<img align="right" alt="Sales Management Analysis" width="1000" height = "400" src="https://monday.com/blog/wp-content/uploads/2021/05/sales-analysis.jpg">

---


# Table of Contents

- [Introduction](https://github.com/globalsmile/Olympics-Games-Analysis#introduction)
- [Problem Statement](https://github.com/globalsmile/Olympics-Games-Analysis#Problem-Statement)
- [Data Sourcing](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Sourcing)
- [Data Preparation](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Preparation)
- [Data Modeling](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Modeling)
- [Data Visualization](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Visualization)
- [Data Analysis & Insights](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Analysis)
- [Shareable link](https://github.com/globalsmile/Olympics-Games-Analysis#Shareable-Link)


---

# Introduction

The Summer Olympic Games (French: Jeux olympiques d'été), also known as the Games of the Olympiad, and often referred to as the Summer Olympics, is a major international multi-sport event normally held once every four years. The inaugural Games took place in 1896 in Athens, Greece, and the most recent edition was held in 2021 in Tokyo, Japan. The International Olympic Committee (IOC) is responsible for organising the Games and for overseeing the host city's preparations. The tradition of awarding medals began in 1904; in each Olympic event, gold medals are awarded for first place, silver medals for second place, and bronze medals for third place. The Winter Olympic Games were created out of the success of the Summer Olympic Games, which are regarded as the largest and most prestigious multi-sport international event in the world...
[Read More](https://en.wikipedia.org/wiki/Summer_Olympic_Games)



---

# Problem Statement

The purpose of this Olympic Games analysis is to visualize data that will help readers understand how countries have performed historically in the summer Olympic Games(with the possibility to select your own country).
There is also an interest in the details about the competitors.



---

# Data Sourcing

- The Dataset used for this analysis is available at [Olympic Games dataset](https://www.dropbox.com/s/3sxwx52o3x8ozj7/olympic_games.bak?dl=0) 


---

# Data Preparation

Data cleaning and transformation was done in Microsoft SQL Server and the datasets was loaded into Microsoft Power BI Desktop for modeling.

The Olympics Game dataset is contained in a table named:

- `Olympic_Data` which has `10 columns and 222,552 rows` of observation

The necessary data was first put into a SQL database and afterwards transformed using the transformations that you can see below.

`Olympic_Data`

```TSQL
SELECT
         [Name] AS 'Competitor Name'
        ,CASE WHEN SEX = 'M' THEN 'Male' ELSE 'Female' END AS Sex
        ,[Age]
		,CASE	WHEN [Age] < 18 THEN 'Under 18'
				WHEN [Age] BETWEEN 18 AND 25 THEN '18-25'
				WHEN [Age] BETWEEN 25 AND 30 THEN '25-30'
				WHEN [Age] > 30 THEN 'Over 30'
		 END AS [Age Grouping]
        ,[Height]
        ,[Weight]
        ,[NOC] AS 'Nation Code'
        ,LEFT(Games, CHARINDEX(' ', Games) - 1) AS 'Year' 
        ,[Sport]
        ,CASE WHEN Medal = 'NA' THEN 'Not Registered' ELSE Medal END AS Medal 
  FROM [olympic_games].[dbo].[athletes_event_results]
  WHERE RIGHT(Games,CHARINDEX(' ', REVERSE(Games))-1) = 'Summer'
```

The tabulation below shows the `Olympic_Data` table with its column names and their description:
| Column Name | Description |
| ----------- | ----------- |
| Competitor Name | Describes the competitors name |
| Sex | Describes the competitors gender |
| Age | Represents the competitors age |
| Height | Represents the competitors height |
| Weight | Represents the competitors weight |
| Nation Code | Describes the competitors nationality |
| Year | Represents the year of the Olympic Games |
| Season | Describes the season of the Olympic Games |
| Sport | Describes the sport the competitor participated in |
| Medal | Describes the medal won by the competitor |

---

# Data Modeling

After the dataset was cleaned and transformed, it was ready to be modeled(using Power BI Desktop).

- The fact and dimension have been combined into one table and is shown in the data model below

<img align="right" alt="Data Model" width="1000" height = "400" src="hhttps://user-images.githubusercontent.com/106287208/189198226-fc53789b-a1ea-4b31-9a5b-0f5184aa6a1d.png">

---

# Data Visualization

Data visualization for the datasets was done in 3 folds using Microsoft Power BI Desktop:

- The `Sales Overview`: Shows the sales vs budget KPI, sales by top 10 customers, sales by top 10 products, e.t.c
-  The `Customer Details`: Shows customer specific information
-  The `Product Details`: Shows product specific information


Figure 1 shows visualizations from `Sales Overview` page

| Figure 1 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/188423026-e1b4d76d-ffcc-4f8c-a1b7-bd363922f524.png) |

Figure 2 shows visualizations from `Customer Details` page

| Figure 2 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/188423353-266e6a75-d31a-4f2e-ba1d-30dd1f591050.png) |

Figure 3 shows visualizations from `Product Details` page

| Figure 3 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/188423526-fe1c6dd3-73da-4f8f-b757-5d585be1eec3.png) |

---

# Data Analysis & Insights

Measures used in visualization are:

- Budget = `SUM ( FACT_Budget[Budget] )`
- Sales = `SUM ( FACT_InternetSales[SalesAmount] )`
- Sales / Budget = `[Sales] - [Budget]`


As shown from [Data Visualization](https://github.com/globalsmile/Sales-Management-Analysis#Data-Visualization), It can be deducted that for the year ending December 2021:

- Sales is up by `1,051,550`
- The top customer by sales is `Jordan Turner`
- The top product by sales is `Mountain-200 Black,42`
- The top product category by sales is the `Bikes` occupying 93.93% of the total sales
- There is a positive correlation between `Sales` and `Budget`

---

# Shareable Link

You can interact with the report here: 

[Report](https://app.powerbi.com/view?r=eyJrIjoiNWVmNDRjNjEtNjZjZC00OGE2LTllYjktMDRjMmMyOTE4ZDYxIiwidCI6IjQ5ODY4YWYzLWNjNWYtNDIxNC04YjdmLTQwZjM3NDY0OWEwOSJ9)
