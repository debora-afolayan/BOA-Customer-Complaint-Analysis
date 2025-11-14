# **Introduction**


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

1.**Data Understanding & Cleaning**

- Removed Duplicates

- Assigned Correct Data Types

- Standardized inconsistent product names and categories.

- Validated dates for Date received and Date submitted.

- Created a unified Date Table to support time intelligence analysis.

- Created a State Dimension Table 

- Created Year Dimension Table

- Removed blank complaint IDs and duplicate entries.

- Ensured all complaint records were linked correctly to states, products, issues, and response outcomes.

2. **Data Modeling**
**A Star Schema was created**
Fact Table

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
DateTable


Product Dimension


State/Region Dimension


Issue Category Dimension


Relationships were created between Fact_Complaints and the DateTable using Date Received.
