# Enquiry Analytics for FY23

The report presents a snapshot of customer enquiries received by the e-commerce firm in Indian fiscal year 2022-23 (FY23 - April 1, 2022 to March 31, 2023).

## Table of Contents
1. [Background and Assumptions](#background-and-assumptions)
2. [Enquiry Analytics](#enquiry-analytics)
   * [Relationship Model](#relationship-model)
   * [Enquiry Analytics Report](#enquiry-analytics-report)
   * [Drilling Down](#drilling-down)
3. [Business Observations and Inferences](#business-observations-and-inferences)
4. [Business Recommendations](#business-recommendations)
   * [Short-Term](#short-term)
   * [Medium-Term](#medium-term)
   * [Long-Term](#long-term)
5. [Limitations](#limitations)
6. [Conclusion](#conclusion)

## Background and Assumptions
An enquiry is generated when a customer requires a product for his/her construction site. The customer is assigned a salesperson, and factors like product requirements, site location, delivery date and customer budget are discussed.  It is the first step in the business transaction. The calculations and logic involved behind creating the enquiries in this analysis have been dealt with in detail in the folder named "Data Modelling".  

Some context and assumptions behind this report are as follows:
1. The analysis pertains to the Chennai region (Chennai city and surrounding urban agglomeration) for the period of April 1, 2022 to March 31, 2023
2. Products under 4 categories are dealt with namely Cement, AAC Blocks, Steel and Concrete
3. A total of 500 customers have generated 5,944 enquiries in the period under consideration
4. The customers are handled by 10 salespersons
5. Each enquiry is assumed to correspond to one product
6. Sundays, holidays and days affected by Cyclone have been assumed to have zero enquiries
7. Postal Pincode has been taken as the proxy for the location of the construction site for which the enquiry is being generated, and need not be identical to the actual address of the customer
8. Minimal AI assistance has been used in this project, particularly for the following:
   * Mockarooo to generate customer names
   * ChatGPT to check for mathematical errors and inconsistencies, and assist in handling Excel formulae and DAX queries. The DAX queries have been uploaded in this folder.

## Enquiry Analytics
The file named "Enquiries Analytics for FY23.pbix" contains an interactive PowerBI dashboard to analyse the enquiries received on FY23. The interactive dashboard cannot be embedded here thanks to Microsoft's rigid account policies.  

### Relationship Model
The star schema is as follows: 

<img width="1473" height="653" alt="image" src="https://github.com/user-attachments/assets/4f036bd6-3ee0-438d-8985-bc8c7e5cb785" />  


|	Column (From Table)	|	Column (To Table)	|	Cardinality	|	Cross-filter Direction	|
|	------	|	------	|	------	|	------	|
|	Customer ID (Enquiry Master)	|	cust_id (Customer Master)	|	Many to one (*:1)	|	Single	|
|	Assigned To (Enquiry Master)	|	Employee Name (Sales Team)	|	Many to one (*:1)	|	Single	|
|	Product (Enquiry Master)	|	Item Name (Product Master)	|	Many to one (*:1)	|	Single	|
|	Assigned Date (Enquiry Master)	|	Date (Calender Master)	|	Many to one (*:1)	|	Single	|
|	Location (Enquiry Master)	|	Area (Enquiry Pincode)	|	Many to one (*:1)	|	Single	|

Thus the relationships were mapped between the tables.

### Enquiry Analytics Report
A screenshot of the report has been pasted below:
<img width="2075" height="1200" alt="Enquiries Analytics for FY23_page-0001" src="https://github.com/user-attachments/assets/f917aa35-57f3-4ba2-a01f-29bc39bbc69c" />


A concise explanation of the visuals is given below:
1. The top consists of the title bar
2. The Key Performance Indicators (KPIs) are placed in the top left below the title bar, consisting of:
   * Total enquiries generated in the period under consideration
   * Total customers in the period under consideration
   * Enquiries as of the most recent date, compared to the previous date
   * Month-to-Date (MTD) enquiries as of the most recent date, compared to the same day in the previous month 
3. Two filters are placed on the top right below the title bar:
   * Salesperson: To help filter salesperson level data, which would be useful for review meetings
   * Calendar Slicer: To filter data across periods to aid in useful analyses
4. Monthly Enquiries: A visual explaining the monthly variation of the number of enquiries is presented here. The visual can be drilled down to the day level
5. Top 10 Customers: A leader-board of the customers generating highest number of enquiries, along with the corresponding salesperson is shown here
6. Enquiries by Location: The geographical spread in the number of enquiries is shown in a bubble chat
7. Enquiries by Product Category: The breakup of enquiries as per products preferred by the customers is revealed here
8. Enquiries by Customer Type: The B2B vs B2C breakup of customers is illustrated here

### Drilling Down
The monthly enquiries chart can be drilled down to the day level. For instance, the enquiry statistics for the month of February is presented here:
<img width="2075" height="1200" alt="February Daily Analytics_page-0001" src="https://github.com/user-attachments/assets/61937219-959e-455d-85bd-eac277addd89" />

The interactions can be clearly seen in this report when the user wants to probe one aspect of a chart deeply.  

## Business Observations and Inferences
From the report, the following observations can be made:
1. Monthly Trends
   1. The business reflects a general rising trend, with dips seen in September-October and December.
   2. The September-October dip seems to be consistent with the numbers in April-June, and the high in August is the likely anomaly
   3. The high in August appears to coincide with the fact that the digital marketing campaign was initiated in July. The reach towards the leads was boosted by Facebook as we were its new customer, and that may have contributed to the sudden spike in enquiries. However, the artificial free boost was revoked after August, showing the dip in September.
   4. The December dip is explained by a multitude of external factors:
      * The cyclone Mandous which made landfall which made landfall off the coast of the Bay of Bengal affected the construction industry during 10-12 December, 2022
      * According to local custom, new projects are not generally initiated in the Tamil month of Margazhi (December 16, 2022 to January 14, 2023). This led to reduced demand.
      * Other festivals like Christmas and New Year, and general monsoon conditions (Northeast Monsoon) affected demand in the construction sector during this period
   5. The dip in December continued until the festival of Pongal (January 14-16, 2023). However, the actual rise in demand was revealed in February.
   6. Post-Pongal, the business continued in its general rising trend
2. The first 4 of the top 10 customers are tied at 60. However, no customer has ever crossed the three digit mark (100 enquiries) in a single year
3. Geographical Trends
   1. The areas close to Tambaram have larger bubbles, thanks to a construction boom in the region.
   2. Larger bubbles are also seen in the East Coast Road (ECR) region (like Sholinganallur), as well as in areas of new Metro Rail constructions (like Valasaravakkam)
   3. The bubbles are smaller in interior Chennai city (as seen in Chepauk and Chintadripet), reflecting lower demand for construction projects
   4. The areas to the northwest around Avadi and Villivakkam have virtually zero enquiries, which is also seen in the region between Tambaram and ECR
4. Trend by Product Category
   1. Cement is the dominant product, closely followed by AAC blocks
   2. Steel and Concrete enquiries need more catching up 
5. Trend by Customer Type
   1. There is a clear bias towards B2C transactions, as only 1/3rd of the enquiries come from firms (B2B)

## Business Recommendations
The following are the recommendations for the business to maintain the momentum and prevent the crises seen in the report:
### Short-Term
1.  A higher investment in digital marketing can boost enquiries, as seen in the increase in number of enquiries on August.
2.  The most loyal customers can be rewarded with discounts, freebies or vouchers (like gifts or vacation tickets).
3.  The region between Tambaram and ECR, as well as the region to the northeast of Chennai desperately need more marketing and outreach by the company. This can be done through cold calls, salesperson visits and targeted digital marketing
### Medium-Term
1. A dip was seen during Cyclone Mandous and in days with heavy rains. Customers can be given an option to insure their products with an additional charge, thus incentivising them to conduct more transactions with our firm. A tie up with potential insurance firms may be explored in this regard.
2. Steel and concrete sales are the 'cash cows' of the construction sector and will lead to higher margins for the business. A more aggressive campaign is required to onboard customers to buy these products.
3. Customers can be segmented based on age, gender (if individual), locality and budget, and schemes can be targeted accordingly.
4. Re-acquisition of customers who haven't submitted enquiries for more than 3 months can be prioritised, via cold calls or targeted ads.
### Long-Term
1. Business-to-business (B2B) transactions should be aggressively targeted, and top-level meetings and contracts can be considered to establish relationships with construction firms.
2. The dip due to seasonal and cultural factors (as seen in Margazhi month) can be potentially arrested by exploring contract relationships with customers, wherein the business provides construction products to the customer for the duration of the whole project in exchange for benefits like prioritised delivery or discounts. 


# Limitations
1. Due to synthetic nature of the data, some numbers can appear to be dramatic. For instance, the visual named "Top 10 Customers" contains 4 customers tied at 60 enquiries.
2. Price analytics has been omitted for simplicity
3. Product level data has not been considered in this analysis, and quantities have been omitted for simplicity
4. Pincodes do not show a reliable geographical spread as multiple enquiries can get concentrated in one bubble

However, the data is fictional and constructed according to the best of my knowledge using human judgement without assistance from other individuals or AI to create the numbers or simulate real-world constraints and chaos. 

# Conclusion
The business shows a general trend in the number of enquiries, with 5,944 enquiries being generated by customers in FY23. Trends in enquiries by the month, locality, customer and product were identified. Based on the observations from the report, actionable insights were recommended to maintain existing momentum and prevent the dips seen in FY23. With the availability of new and further data, a more comprehensive analysis can be made.

Feel free to contact me for queries and feedback!
