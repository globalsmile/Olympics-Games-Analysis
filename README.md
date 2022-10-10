# Olympics Games Analysis

<img align="right" alt="Sales Management Analysis" width="1000" height = "400" src="https://st.depositphotos.com/2461721/4028/i/450/depositphotos_40285597-stock-photo-olympic-rings.jpg">

---


# Table of Contents

- [Problem Statement](https://github.com/globalsmile/Olympics-Games-Analysis#Problem-Statement)
- [Data Sourcing](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Sourcing)
- [Data Preparation](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Preparation)
- [Data Modeling](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Modeling)
- [Data Visualization](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Visualization)
- [Data Analysis & Insights](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Analysis)
- [Shareable link](https://github.com/globalsmile/Olympics-Games-Analysis#Shareable-Link)


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

- `Olympic_Data` which has `11 columns and 222,552 rows` of observation

The necessary data was first put into a SQL database and afterwards transformed using the transformations that you can see below.

`Olympic_Data`

```TSQL
SELECT
         [ID]
        ,[Name] AS 'Competitor Name'
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
| ID | Represents the number of competitors |
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

<img align="right" alt="Data Model" width="1000" height = "400" src="https://analyzewithaliportfolio.files.wordpress.com/2021/08/olympicgamesanalysis3.png">

---



# Data Visualization

Data visualization for the dataset was done using Microsft Power BI Destop:

- The `Olympic Games Analysis` Page: Shows the # of competitors, # of Medals, # of medals by year, etc

Figure 1 shows visualizations from `Olympic Games Analysis` page

| Figure 1 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/189209800-f64b107b-2a4e-4562-a042-3dd7fc414721.png) |

---

# Data Analysis & Insights

Measures used in visualization are:

- '# of Competitors' = `DISTINTCOUNT ( 'Olympic_Data[ID] )`
- '# of Medals' = `COUNTROWS ( 'Olympic_Data' )`
- '# of Medals (Registered)' = `CALCULATE ([# of Medals], FILTER( 'Olympic_Data', 'Olympic_Data'[Medal] = "Bronze" || 'Olympic_Data' [Medal] = "Gold" || 'Olympic_Data'[Medal] = "Silver")`


As shown from [Data Visualization](https://github.com/globalsmile/Olympics-Games-Analysis#Data-Visualization), It can be deduced that:

- From 1896-2016, the total number of competitors is `116,776`
- From 1896-2016, the total number of medals received is `34,088`

---

# Shareable Link

You can interact with the report here: 

[Report](https://app.powerbi.com/view?r=eyJrIjoiMDdkMzY4NTYtZTE5Ny00ZTBkLTk4OWYtOGUxYmExZGViM2IyIiwidCI6IjQ5ODY4YWYzLWNjNWYtNDIxNC04YjdmLTQwZjM3NDY0OWEwOSJ9)
