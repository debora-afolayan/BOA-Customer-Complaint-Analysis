# **Introduction**

**Introduction**

This project analyzes consumer complaint data submitted to Bank of America to identify key trends, patterns, and drivers behind customer issues. By examining complaint categories, response types, resolution timeliness, and customer sentiment, the analysis provides insights that support better service delivery, operational efficiency, and data-driven decision-making. The goal is to help stakeholders understand where complaints originate, how effectively they are resolved, and what opportunities exist to improve the overall customer experience.

# **Project Description**

This project focuses on end-to-end analysis of Bank of America consumer complaint data. It covers the full workflow, including data import, cleaning, quality checks, and transformation using Power Query; exploratory data analysis using Power BI and Excel; and the creation of interactive dashboards that highlight complaint trends, response behaviors, and resolution performance. The approach is designed to answer key business questions—such as which issues customers report most frequently, how the bank responds, and how timely resolutions are—while providing insights and recommendations that guide service improvement and operational decision-making.


# **Project Aim**

To analyze Bank of America’s consumer complaint data to identify key trends, understand customer pain points, evaluate the bank’s response performance, and provide actionable insights that support improved customer service and operational decision-making.


# **About the Dataset**


The dataset used for this project is sourced from the Consumer Financial Protection Bureau (CFPB) public complaint database, which contains customer-submitted complaints about financial institutions, including Bank of America. The extracted dataset focuses specifically on complaints related to Bank of America.

It contains approximately 65,000 rows and 12 columns, providing detailed information about each customer complaint.

**Key Fields/Columns include:**

- Complaint ID – Unique identifier for each complaint

- Date Submitted – When the compliant was submitted

- Date Received – When the complaint was received

- Product – The financial product or service involved (e.g., credit card, mortgage)

- Sub-product 

- Issue – Specific problem experienced by the customer

- Sub-Issue  

- Company Response to consumer – BOA's response to customer

- Company Response to public – BOA's response to the public

- State – Customer location

- Submitted Via – Channel used to submit the complaint (e.g., web, phone)

- Timely Response


# **Tools Used**


- Excel (Power Query)
- PowerBi (Dax, Data Modelling, Visualization) 


# **Analysis & Methodology**


To address the business problems and answer stakeholder questions, a comprehensive analysis was conducted on Bank of America’s CFPB customer complaint dataset (2017–2023). The process included data cleaning, data modeling, measure creation, visual analytics, and predictive forecasting.

**The analysis followed these stages:**

**1. Data Understanding & Cleaning**

- Removed Duplicates

- Assigned Correct Data Types

- Standardized inconsistent product names and categories.

- Validated dates for Date received and Date submitted.

- Created a unified Date Table to support time intelligence analysis.

- Created a State Dimension Table 

- Created Year Dimension Table

- Removed blank complaint IDs and duplicate entries.

- Ensured all complaint records were linked correctly to states, products, issues, and response outcomes.

**2. Data Modeling**

**A Star Schema was created**

**Fact Table**

- Fact_Complaints

- Complaint ID

- Product

- Issue

- Region / State

- Submission Channel

- Date Received

- Date Submitted

- Response Type

- Timely Response Flag (Yes/No)


**Dimension Tables**

- DateTable

- State/Region Dimension

- Issue Category Dimension

- Relationships were created between Fact_Complaints and the DateTable using Date Received.


**3. DAX Measures Used to Produce Insights**

**📌 Base Measures**

- **Total Complaints =** COUNTROWS('Fact_Complaints')

- **Total Complaints (Monthly) =**
CALCULATE([Total Complaints], ALLEXCEPT('DateTable','DateTable'[YearMonth]))

- **Total Complaints (Yearly) =**
CALCULATE([Total Complaints], ALLEXCEPT('DateTable','DateTable'[Year]))

**📌 Complaint Trend Analysis**

- **Last Actual Year =**
CALCULATE(MAX('DateTable'[Year]),
FILTER(ALL('DateTable'), NOT ISBLANK([Total Complaints])))

- **Total Complaints (Last Year) =**
CALCULATE([Total Complaints], 'DateTable'[Year] = [Last Actual Year] - 1)

- **YoY % Change =**
DIVIDE([Total Complaints] - [Total Complaints (Last Year)], [Total Complaints (Last Year)])

**Used to generate year-over-year trend charts and KPI cards.**

**📌 Response Performance**

- **Timely Response % =**

DIVIDE(
    CALCULATE([Total Complaints], 'Fact_Complaints'[Timely response] = "Yes"),
    [Total Complaints])

- **Customer Satisfaction % =**
CALCULATE( DIVIDE( CALCULATE([Total Complaints], 'Fact_Complaints'[Consumer disputed] = "No"),[Total Complaints] ))

These supported visuals on response quality, timeliness, and resolution outcomes.

**📌 Geographical Insights**

- **Complaints by State** = [Total Complaints]

- **Complaints by Region =**
CALCULATE([Total Complaints], ALLEXCEPT('Fact_Complaints','Fact_Complaints'[Region]))

Used to render the state map and regional breakdown.


**📌 Forecasting (Next 2 Years)**

**Growth for forecasting:**
- **Complaint Growth Rate =**

- **VAR Last =** [Last Actual Year]

- **VAR Current =** CALCULATE([Total Complaints], 'DateTable'[Year] = Last)

- **VAR Previous =** CALCULATE([Total Complaints], 'DateTable'[Year] = Last - 1)
RETURN DIVIDE(Current - Previous, Previous)

**Forecast year + 1:**

**Forecast Next Year =**

- **VAR LastValue =** CALCULATE([Total Complaints], 'DateTable'[Year] = [Last Actual Year])
RETURN LastValue * (1 + [Complaint Growth Rate])

**Forecast year + 2:**

**Forecast Year After Next =**

- **VAR NextYearValue =** [Forecast Next Year]
RETURN NextYearValue * (1 + [Complaint Growth Rate])

**These were displayed in KPI cards:**

- **Total Number of Complaints**

- **Complaint Response Rate**

- **Customer Satisfaction Rate**

- **Year on Year % Change in Complaints**

- **Forecast 2024**

- **Forecast 2025**

- **Two-Year Growth %**


# **Complaint Analysis Overview Dashboard**


**KPI Cards:** - Total Number of Complaints, Complaint Response Rate, Customer Satisfaction Rate, Year on Year % Change in Complaints.

**Bar Chart:** Top Products with Complaints, Top Complaint Channels .

**Line Chart:** Yearly Complaint Trend.

**Column Chart:** Complaint Response Status, Top 10 Customer Issues.


# **Geographical Analysis Dashboard**


**Funnel:** Regions by Complaint Distribution.

**Map:** Top 5 States by Complaints.

**Column Chart:** Top 20 States by complaints count, Average number of Days for BOA to receive complaint after complaint Submission by Customer.


 # **Predictive Analysis Dashboard**


**KPI Cards:** - 2022 Total Complaints, 2023 Total Complaints, 2024 Forcast number, Year on Year % Change in Complaints, 2 years Time Forcast number growth.

**Decomposition Tree:** Complaint distribution by Product, Year, Region and Complaint Channel .

**Line Chart:** Complaint Forcast  by Year and Months.

**Column Chart:** Complaint Response Status, Top 10 Customer Issues.


# **Executive Summary**

This analysis evaluated 62,000+ customer complaints submitted to the CFPB regarding Bank of America from 2017 to 2023. The goal was to provide leadership with a data-driven understanding of what customers complain about, where complaints originate, how effectively the bank responds, and what future complaint levels may look like.

The analysis revealed that complaints are heavily concentrated around Savings Accounts, Credit Cards, and Credit Reporting, with the South and West regions recording the highest volumes. While the bank maintains strong response outcomes, with 97.6% of customers indicating no dispute, there are notable variations in response timeliness across regions.

Customers primarily use web and referral channels to submit complaints, indicating a shift toward digital engagement. Forecasting models show that, if current patterns continue, complaint volumes may continue to rise modestly over the next two years.
The findings provide clear direction for improving service delivery, product experience, and operational efficiency.

# **🔍 Key Insights**

1. Savings Accounts, Credit Cards & Credit Reporting are the top complaint drivers
These three products consistently account for over half of all complaints.

2. “Managing Account”, “Incorrect Information”, and “Billing Issues” are the most recurring issues
These reflect underlying problems in account servicing, billing disputes, and data accuracy.

3. The South and West regions show the highest complaint concentration
California leads as the state with the highest complaint volume.

4. Web and Referral channels dominate complaint submission
Indicates a preference for self-service and digital engagement over phone or mail.

5. Strong satisfaction and closure performance
97.6% of customers did not dispute the response. Most complaints were closed with explanation, showing effective resolution.

6. Timeliness of response varies across regions
Some regions take significantly longer to respond, indicating operational inefficiencies.

7. Complaint levels show a fluctuating trend from 2017 to 2023
YoY trends reveal spikes in certain years linked to economic and operational factors.

8. Forecast indicates continued decrease in complaints through 2024–2025
If current patterns hold, complaint volume will show a gradual decrease over the next two years.


# **✔ Recommendations**


**1. Prioritize improvement in top complaint productsFocus on:**

- Savings Account servicing

- Credit Card dispute handling

- Credit Reporting accuracy

This will reduce overall complaint volumes significantly.

**2. Address root causes of top issues**

**Establish targeted initiatives for:**

- Billing system improvements

- Fraud detection enhancements

- Better account management support

- Customer data accuracy controls

**3. Improve operational efficiency in slow-response regions**

Standardize response protocols and allocate more back-office resources where needed.

**4. Enhance digital self-service channels**

**Since customers prefer web submission:**

- Improve complaint submission UI

- Add self-resolution tools

- Implement status notifications

-Provide real-time tracking

**5. Strengthen monitoring and early-warning analytics**

**Use:**

- Monthly trend monitoring

- Decomposition Tree for root cause identification

- Forecast KPIs to anticipate high-volume periods


**6. Increase training for customer-facing and dispute-resolution teams**

- Particularly in product areas with high complaint volumes and recurrent issues.

**7. Implement product-specific customer feedback loops**

- Collect feedback post-resolution to reduce repeat complaints and increase satisfaction.


