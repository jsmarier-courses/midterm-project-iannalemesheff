**2024-11-04**<br>
**MPAD2003A Introductory Data Storytelling**<br>
**Ianna Lemesheff**<br>
**Presented to Jean-Sébastien Marier**<br>

repo link: https://github.com/jsmarier-courses/midterm-project-iannalemesheff

# Midterm Project: Exploratory Data Analysis (EDA)

<!-- Use one hashtag symbol (`#`) to create a level 1 heading like this one. -->

## Foreword

For this assignment, you must extract data from a dataset provided by the instructor. You must then clean and analyze the data, create exploratory charts/visualizations, and find a potential story idea. Your assignment must clearly detail your process. You are expected to write about 1500-2000 words, and to include several screen captures showing the different steps you went through. Your assignment must be written with the Markdown format and submitted on GitHub Classroom.

I have been assigning different versions of this project to my digital journalism and data storytelling students for a few years now. Its structure was inspired by the main sections/chapters of [*The Data Journalism Handbook*](https://datajournalism.com/read/handbook/one/). This version was further inspired by the [Key Capabilities in Data Science](https://extendedlearning.ubc.ca/programs/key-capabilities-data-science) program offered by the University of British Columbia (UBC).

**Here are some useful resources for this assignment:**

* [GitHub's *Basic writing and formatting syntax* page](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
* [The template repository for this assignment in case you delete something by mistake](https://github.com/jsmarier/jou4100_jou4500_mpad2003_project2_template)

Did you notice how to create a hyperlink? In Markdown, we put the clickable text between square brackets and the actual URL between parentheses.

And to create an unordered list, we simply put a star (`*`) before each item.

## 1. Introduction

I will be analyzing a dataset collected by the City of Ottawa, which provides a summary of service requests made to the city in the year 2024. According to their website, the data was collected from 311 calls, the client service centre and an online self-service portal. Noteable data categories include:
* The category of the request
* Description of the request
* Dates of the request
* Status of the request

**Data sources:**
[2024 Service Requests (City of Ottawa)](https://open.ottawa.ca/documents/65fe42e2502d442b8a774fd3d954cac5/about)
[Jean-Sebastien Marier's .csv file](https://raw.githubusercontent.com/jsmarier/course-datasets/refs/heads/main/ottawa-311-service-requests-august-2024.csv)


## 2. Getting Data

To start, import your data into Google Sheets following these steps:
1. File > Import
1. Upload your .csv file from your computer.
1. Import Location: Choose where you want your new spreadsheet to be imported. 
1. Separator Type: Since we are working with a .csv (comma-separated values), pick commas as your separators.
1. Hit the Import Data button.

**Your spreadsheet should look like this.**

![](getting-data.png)<br>
*Figure 1: The spreadsheet when imported.*

Columns: 11
Rows: 28,539

The newly imported spreadsheet does not look very nice. At first glance, columns are not wide enough and it is hard to identify the column labels.

[Link to my sample spreadsheet](https://docs.google.com/spreadsheets/d/1ZEO05kqe66DBUfp4FLY0f9Z0KFAh6NdQquYK_CJBdo8/edit?usp=sharing)

You will notice that my spreadsheet looks quite different compared to the picture. That is because I cleaned it. I will explain my cleaning techniques in the upcoming section.

**Some observations about the data:**
* Column B features the status of the service request as nominal data*. The three categories included are: resolved, active, and cancelled.
* Column C features the type of service request made by the complainant. This is again, categorical nominal data, with more categories listed this time. The categories of service requests include: bylaw services, citizen services, city facilities, garbage & recycling, health & safety, licenses and permits, parking control enforcement, recreation & culture, roads & transportation, social community service, and water & the environment.
* Column J features the ward in which the service request was made. Despite the data being a range of numbers, it is still categorical nominal data, as each number is just a stand in for the ward name. Wards range from 1-24.
* Column H & I detail the latitude and longitude of the location related to the complaint. Both variables are continuous values.**

***Nominal data** is a form of categorical data. It is described as non-quantifiable data that does not have an order associated with it.
****Continuous data** is a form of numeric data. It is a quantifiable form of data that has an infinite amount of values within an interval. (Statistics Canada, 2021)


Some data is missing in the table. The columns that have missing data appear to be location data. Some requests are missing addresses and therefore coordinates and ward info. However, some requests have the address/coordinates recorded but do not have the ward filled in. This can be quickly fixed manually by searching up the ward of each address.

A question I have asked myself while skimming through the data is: which ward has the most complaints? Does the number of complaints reflect the population... or does it indicate something else? Perhaps the city councillors are neglecting their ward OR there could be higher community involvement in the area OR a higher rate of delinquency. It could also be a combination of these factors. I will attempt to identify the reason, if any.

## 3. Understanding Data

### 3.1. VIMO Analysis

VIMO stands for Valid, Invalid, Missing, Outlier. Statistics Canada (2020) provides a tutorial on VIMO as an effective list of criteria to determine the general accuracy and quality of a dataset. Let's analyze this spreadsheet using VIMO.

**Valid:** Almost all of the columns appear to be valid. For example, all the dates appear to be within a proper range (August 2024). There are up to 24 wards which reflects the wards listed on the City of Ottawa website. etc.

**Invalid:** I have not identified any definitively invalid data in the spreadsheet.

**Missing:** As previously stated, some rows within the wards column are missing data where the address of the request is known.

**Outlier:** There is one outlier in the data. One of the requests appears to have been made in September. It is possible that they accidentally wrote 9 instead of 8 as the month. But, since the data is on the first of the month, it is likely that one request in the start of September made it into August's data.

### 3.2. Cleaning Data

Here are some methods I used to clean the spreadsheet:

* **Freeze row.** I froze row 1 so that the column labels are always visible.
* **Adjusting column width.** This allows all of the content in the cells to be easily readable, as well as condensing other columns so that more data is visible on the screen at once.
* **Manual cleaning.** I went in and added the missing ward numbers by searching the addresses on [this map](https://data.mapchannels.com/mc3/1369/ottawawards_1369.htm?v=20110211021742).
* **Find and replace.** I used this to display the names of the wards along with the numbers. For example, I would find 1 and change it to 1/Orleans East-Cumberland. Make sure to select "Match entire cell contents". Having the ward names written down in the dataset is good for easy reference.
* **SPLIT.** I used this to split the numbers and names of the wards between the / symbol. I thought keeping the numbers of the wards was important for organization. The formula I used was `=SPLIT(J:J,"/")`. Make sure to cut and paste the new columns as values only before you delete the old column.
* **Delete french text.** You can do this manually in row 1. Use SPLIT to divide the Description column (D). I used the formula `=SPLIT(D:D,"|")`.
* **Delete extra columns.** I deleted Latitude/Longitude because I found that they were unnecessary with the inclusion of the address category. I also deleted the Channel category as it will not be needed for my analysis.

**After cleaning, your spreadsheet should look like this:**

![](understanding-data.png)<br>
*Figure 2: The spreadsheet after cleaning.*

### 3.3. Exploratory Data Analysis (EDA)


![](pivot-table.png)<br>
*Figure 3: This pivot table shows a list of the wards in Ottawa alongside the number of service requests submitted for each one.*

I chose these variables because it relates to my question. I want to know... what ward(s) have the most service requests and why?

To create a table like this, you add the ward no. and the wards as rows. Then, you can add the ward no. as a value and summarize it by COUNTA.

Rideau-Vanier has the highest number of service requests, closely followed by Somerset. These are the only wards that surpassed 1500 requests in August 2024.

It is also worth noting that West Carleton-March, Beacon Hill-Cyrville and Osgoode all appear to have the lowest number of requests, ranging at around 600.


![](chart-screencap.png)<br>
*Figure 4: This exploratory chart shows the no. of service requests as a bar chart.*

The chart makes it significantly easier to quickly identify which wards have the most/least requests. That is because a bar chart utilizes position along a common scale to help the viewer make accurate estimates. This is based on the hierarchy of elementary perceptual tasks, by Cleveland and McGill. 


"...if you wish to create a successful chart, you need to construct it based on elementary tasks “as high in the hierarchy as possible.” The closer you move to the top of the scale, the faster and more accurate the estimates readers can make with your graphic... Area, color, and angle are much less effective than those graphic forms based on positioning objects on common scales." (Cairo, 2016) 

Next, I must try and answer my question by using this table and chart. More specifcally, I want to focus on why Rideau-Vanier and Somerset have the most requests.

## 4. Potential Story

To tell my story about Rideau-Vanier and Somerset, I first need to find some extra information.
* What is the population of these wards relative to the rest of Ottawa?
* Is there a higher crime rate in these areas?
* What are the personal accounts of residents who live in these areas? Do they agree with the type of requests made?

I could also create new charts specific to the wards to make new connections. For example, I could create a chart that shows the frequescy of each type of request made in these two wards, to determine which problems it faces the most.

[This chart](https://ottawa.ca/en/living-ottawa/statistics-and-demographics/current-population-and-household-estimates#section-f580706c-6d2d-41eb-9977-34b60d1e633f) on the City of Ottawa website details the population of each ward. At first glance, neither Rideau or Somerset have the highest populations. This can indicate that there is a higher volume of problems in the area. One could infer that as these areas are located in/nearby the downtown core, that there is a higher number of visitors, a higher number of people living on the streets, a higher number of pollution, noise, etc. All of these are issues that people bring up to bylaw.

[This article](https://ottawa.ctvnews.ca/these-ottawa-wards-had-the-highest-and-lowest-crime-rates-in-2022-1.6454631#:~:text=There%20were%203%2C160%20crimes%20per,Rideau-Rockcliffe%20and%20Alta%20Vista.) by CTV News states that both these wards have the highest crime rates in Ottawa per 100,000 residents. This is another lead to our story.

Finally, interviewing residents and frequent visitors in these areas will help us paint a more detailed and personal story, supported by quotes. Otherwise, more research must be done to find reliable sources provided by city services such as the Ottawa Police and Ottawa by-law services. This story could help us bring pressing issues to the attention of city councillors Stephanie Plante and Ariel Troster and improve the lives of Ottawa citizens.

## 5. Conclusion

What I found most challenging about this assignment was cleaning the data. It was the most time-consuming task. There was a lot of data, however this task was made easier by the fact that it was already relatively clean.

What I found the most rewarding was discovering that my story/hypothesis could actually work with a little more research. It makes me feel like open data is a powerful tool for discovering new stories.

I realized that I truthfully do not know much about how the municipal government functions. In order for me to tell a quality story, I must understand exactly what city councillors do and what their role is in addressing complaints, crime, etc.

Next time, I will work on my procedural writing skills and include more screenshots in order to create a comprehensive tutorial that absolute beginners could use to analyze datasets.

## 6. References

https://www150.statcan.gc.ca/n1/edu/power-pouvoir/toc-tdm/5214718-eng.htm

https://www.statcan.gc.ca/en/wtc/data-literacy/catalogue/892000062020008

https://learning.oreilly.com/library/view/the-truthful-art/9780133440492/


Include a list of your references here. Please follow [APA guidelines for references](https://apastyle.apa.org/style-grammar-guidelines/references). Hanging paragraphs aren't required though.

**Here's an example:**

Bounegru, L., & Gray, J. (Eds.). (2021). *The Data Journalism Handbook 2: Towards A Critical Data Practice*. Amsterdam University Press. [https://ocul-crl.primo.exlibrisgroup.com/permalink/01OCUL_CRL/hgdufh/alma991022890087305153](https://ocul-crl.primo.exlibrisgroup.com/permalink/01OCUL_CRL/hgdufh/alma991022890087305153)
