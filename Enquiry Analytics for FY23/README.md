# Enquiry Analytics for FY23

The report presents a snapshot of customer enquiries received by the e-commerce platform during Indian fiscal year 2022-23 (FY23 - April 1, 2022 to March 31, 2023).

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
An enquiry is generated when a customer requires a product for his/her construction site. The customer is assigned a salesperson, and factors like product requirements, site location, delivery date and customer budget are discussed.  It is the first step in the business transaction. The calculations and logic involved behind creating the enquiries in this analysis have been dealt with in detail in the folder named [Data Modelling](../Data%20Modelling).  

Some context and assumptions behind this report are as follows:
1. The analysis pertains to the Chennai region (Chennai city and surrounding urban agglomeration) for the period of April 1, 2022 to March 31, 2023
2. Products under 4 categories are dealt with namely Cement, AAC Blocks, Steel and Concrete.
3. A total of 500 customers have generated 5,944 enquiries in the period under consideration.
4. The customers are handled by 10 salespersons.
5. Each enquiry is assumed to correspond to one product.
6. Zero enquiries have been assumed for Sundays, holidays and on the days affected by a Cyclone.
7. Postal Pincode has been taken as the proxy for the location of the construction site for which the enquiry is being generated, and need not be identical to the actual address of the customer.
8. Minimal AI assistance has been used in this project, particularly for the following:
   * Mockarooo to generate customer names
   * ChatGPT to check for mathematical errors and inconsistencies, and assist in handling Excel formulae and DAX measures. The DAX measures have been uploaded in this folder.

## Enquiry Analytics
The file named "Enquiries Analytics for FY23.pbix" contains an interactive Power BI dashboard to analyse the enquiries received on FY23. The interactive Power BI report cannot be embedded here due to Microsoft's work account policies, and thus the relevant screenshots have been posted here.  

### Relationship Model
The star schema is as follows: 

<img width="1292" height="645" alt="Enquiry Star Schema" src="https://github.com/user-attachments/assets/c19d3e77-7153-4b7f-b305-09ea890f0ae3" />


|	Column (From Table)	|	Column (To Table)	|	Cardinality	|	Cross-filter Direction	|
|	------	|	------	|	------	|	------	|
|	Customer ID (Enquiry Master)	|	cust_id (Customer Master)	|	Many to one (*:1)	|	Single	|
|	Assigned To (Enquiry Master)	|	Employee Name (Sales Team)	|	Many to one (*:1)	|	Single	|
|	Product (Enquiry Master)	|	Item Name (Product Master)	|	Many to one (*:1)	|	Single	|
|	Assigned Date (Enquiry Master)	|	Date (Calendar Master)	|	Many to one (*:1)	|	Single	|
|	Location (Enquiry Master)	|	Area (Enquiry Pincode)	|	Many to one (*:1)	|	Single	|

Thus the relationships were mapped between the tables.

### Enquiry Analytics Report
A screenshot of the report has been pasted below:
<img width="2075" height="1200" alt="Enquiries Analytics for FY23_page-0001" src="https://github.com/user-attachments/assets/f917aa35-57f3-4ba2-a01f-29bc39bbc69c" />


A concise explanation of the visuals along with mentions of relevant DAX measures are given below (The DAX measures can be viewed in the respective files as mentioned):
1. The top consists of the title bar
2. The Key Performance Indicators (KPIs) are placed in the top left below the title bar, consisting of:
   * Total Enquiries: Total enquiries generated in the period under consideration
     * A measure named "Total Enquiries" was created which listed the distinct count of enquiries in the "Enquiry Master" sheet
     * Another measure named "Total Enquiries Display" was created to formatting Total Enquiries into thousands with comma separator (#,##0).
   * Total customers
     * Count of customer IDs in the "Customer Master" sheet
   * Enquiries - Most Recent Date: Enquiries as of the most recent date, compared to the previous date
     * Two measures namely "Last Day Enquiries" and "Previous Day Enquiries" were created to return the most recent date and the date before that respectively
     * A measure named "Formatted KPIs" was created to return the Last Day Enquiries and an arrow comparing its trend with Previous Day Enquiries. This measure was displayed on the KPI
     * To obtain colours for rising and falling trends, a measure named "Formatted Color" was created to return Green, Red or Grey colours based on Rising, Falling or Neutral trends respectively
     * To get the title in the format as displayed, a measure named "Enquiries Card Title" was created
   * MTD Enquiries: Month-to-Date (MTD) enquiries as of the most recent date, compared to the same day in the previous month
     * Two measures named "MTD Enquiries" and "Previous MTD Enquiries" were created for comparison
     * A measure named "MTD Formatted KPIs" was created to return the MTD Enquiries and an arrow comparing its trend with Previous MTD Enquiries. This measure was displayed on the KPI
     * To obtain colours for rising and falling trends, a measure named "MTD Formatted Color" was created to return Green, Red or Grey colours based on Rising, Falling or Neutral trends respectively
     * To get the title in the format as displayed, a measure named "MTD Enquiries Card Title" was created
3. Two filters are placed on the top right below the title bar:
   * Salesperson: To help filter salesperson level data, which would be useful for review meetings
     * Filters the report based on "Sales Person" from "Sales Employees" sheet
   * Calendar Slicer: To filter data across periods and help obtain a temporal picture
     * Filters the report based on "Date" from "Calendar Master"
4. Monthly Enquiries: A visual explaining the monthly variation of the number of enquiries is presented here. The visual can be drilled down to the day level
   * X-Axis
     * "Month Name" from "Calendar Master"
       * The X-axis shows the months as per the Indian fiscal year 2023 (FY23)
       * To obtain this measure in Power BI, a new column named "Fiscal Month No" was created to start the months from April (1) and end them on March (12)
       * A column named "Month Name" was created to return only the month of the given date
       * The "Month Name" column was sorted by "Fiscal Month No" to arrange it in the order of months as per the fiscal year
       * This column was selected to represent X-axis
     * The X-axis can be drilled down to the actual "Date" from "Calendar Master"
   * Y-Axis
     * A measure named "Enquiries for Chart" was created to show the enquiry trend line on all days, including those on the x-axis with zero enquiries 
5. Top 10 Customers: A leader-board of the customers generating highest number of enquiries, along with the corresponding salesperson is shown here
   * The column named "Customer Name" shows the actual "Customer Name" from "Customer Master"
   * The column named "Enquiries" counts the number of enquiries from "Enquiry Master" for the customer
   * The column named "Sales Person" shows the salesperson assigned to the enquiry in the "Enquiry Master" sheet
   * The table was then sorted in descending order by number of enquiries, and filtered by Customer ID based on top 10 counts of "Enquiry ID"
6. Enquiries by Location: The geographical spread in the number of enquiries is shown in a bubble chart
   * A measure named "Map Location" was created from "Pincode Master" concatenating the area name, Pincode and "Chennai" into a single string, thus helping Power BI understand the exact location
7. Enquiries by Product Category: The breakup of enquiries as per products preferred by the customers is revealed here
   * The Y-axis shows "Item Name" from "Product Master"
   * The X-axis counts number of enquiries from "Enquiry Master" sheet
8. Enquiries by Customer Type: The B2B vs B2C breakup of customers is illustrated here
   * The legend differentiates the "Customer Type" obtained from "Customer Master"
   * The chart counts number of enquiries from "Enquiry Master" sheet

### Drilling Down
The monthly enquiries chart can be drilled down to the day level. For instance, the enquiry statistics for the month of February is presented here:
<img width="2075" height="1200" alt="February Daily Analytics_page-0001" src="https://github.com/user-attachments/assets/61937219-959e-455d-85bd-eac277addd89" />

## Business Observations and Inferences
From the report, the following observations can be made:
1. Monthly Trends
   1. The business reflects a general rising trend, with dips seen in September-October and December.
   2. The September-October dip seems to be consistent with the numbers observed  in  April-June, and the high in August is the likely anomaly
   3. The high in August appears to coincide with the fact that the digital marketing campaign was initiated in July. The reach towards the leads was boosted by Facebook as e-commerce platform was its new customer, thus contributing to the sudden spike in enquiries. However, the artificial free boost was revoked after August which is reflected by the dip in September.
   4. The December dip is explained by a multitude of external factors:
      * The cyclone Mandous which made landfall which made landfall off the coast of the Bay of Bengal affected the construction industry during 10-12 December, 2022
      * According to local custom, new projects are not generally initiated in the Tamil month of Margazhi (December 16, 2022 to January 14, 2023). This led to reduced demand in the construction sector.
      * Festivals like Christmas and New Year, and general monsoon conditions (Northeast Monsoon) affected demand in the sector during this period
   5. The dip in December continued until the festival of Pongal (January 14-16, 2023). However, the actual rise in demand was revealed by the spike seen from February.
   6. Post-Pongal,  the enquiries continued to follow the general rising trend
2. Top Customers
   1. The first 4 of the top 10 customers are tied at 60.
   2. However, no customer has ever crossed the three digit mark (100 enquiries) in a single year
3. Geographical Trends
   1. The areas close to Tambaram have larger bubbles, thanks to a construction boom in the region.
   2. Larger bubbles are also seen in the East Coast Road (ECR) region (like Sholinganallur), as well as in areas of new Metro Rail constructions (like Valasaravakkam)
   3. The bubbles are smaller in interior Chennai city (as seen in Chepauk and Chintadripet), reflecting lower demand for construction projects in established areas.
   4. The areas to the northwest around Avadi and Villivakkam have virtually zero enquiries, as is the case in the region between Tambaram and ECR.
4. Trend by Product Category.
   1. Cement is the dominant product, closely followed by AAC blocks
   2. Steel and Concrete enquiries however show a significant lag behind the other products.
5. Trend by Customer Type
   1. There is a clear bias towards B2C transactions, as only 1/3rd of the enquiries come from firms (B2B)

## Business Recommendations
The following are the recommendations for the business to maintain the momentum and prevent the crises seen in the report:
### Short-Term
1.  A greater investment in digital marketing can boost enquiries, as seen in the increase in number of enquiries on August.
2.  The most loyal customers can be rewarded with discounts, freebies or vouchers (like gifts or travel vouchers).
3.  The region between Tambaram and ECR, as well as the region to the northeast of Chennai desperately need more marketing and outreach by the e-commerce platform . This can be done through cold calls, salesperson visits and targeted digital marketing initiatives.
### Medium-Term
1. A dip was seen during Cyclone Mandous and in days with heavy rains. To overcome this, the customers can be given an option to add an insurance to their products with an additional charge, thus incentivising them to conduct more transactions with the e-commerce platform. A tie up with potential insurance firms may be explored in this regard.
2. Steel and concrete sales are the 'cash cows' of the construction sector and will lead to higher margins for the platform. A more aggressive campaign is required to onboard customers to conduct transactions in these products.
3. Customers can be segmented based on age, gender (if individual), locality and budget, and schemes can be targeted accordingly.
4. Re-acquisition of customers who haven't submitted enquiries for more than 3 months can be prioritised, via cold calls or targeted ads, thus addressing customer churn..
### Long-Term
1. Business-to-business (B2B) transactions should be aggressively targeted, and top-level meetings and contracts can be considered to establish relationships with construction firms.
2. To reduce the dips caused by seasonal and cultural factors (as seen in the Margazhi month), the e-commerce platform can explore establishing contract relationships with customers, in which the platform provides construction products to the customer for the duration of the whole project in exchange for benefits like prioritised delivery and price discounts.  


# Limitations
1. Due to synthetic nature of the data, some numbers can appear to be dramatic. For instance, the visual named "Top 10 Customers" contains 4 customers tied at 60 enquiries.
2. Price analytics has been omitted for simplicity
3. Product level data has not been considered in this analysis, and quantities have been omitted for simplicity
4. Pincodes do not show a reliable geographical spread as multiple enquiries can get concentrated in one bubble


# Conclusion
The business shows a general trend in the number of enquiries, with 5,944 enquiries being generated by customers in FY23. Trends in enquiries by the month, locality, customer and product were identified. Based on the observations from the report, actionable insights were recommended to maintain existing momentum and prevent the dips seen in FY23. With the availability of new and further data, a more comprehensive analysis can be made.

Feel free to contact me for queries and feedback!
