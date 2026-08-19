# Enquiry Analytics for FY23

The report presents a snapshot of customer enquiries received by the e-commerce firm in Indian fiscal year 2022-23 (FY23 - April 1, 2022 to March 31, 2023).

# Background and Assumptions
An enquiry is the act of a customer where he/she asks for availability of the product, while specifying his/her preferences and negotiating for his/her limitations. It is the first step in the business transaction. The calculations and logic involved behind creating the enquiries in this analysis have been dealt with in detail in the folder named "Data Modelling".  

Some context and assumptions behind this report are as follows:
1. The analysis pertains to the Chennai region (Chennai city and surrounding urban agglomeration) for the period of April 1, 2022 to March 31, 2023
2. Products under 4 categories are dealt with namely Cement, AAC Blocks, Steel and Concrete
3. A total of 500 customers have generated 5,944 enquiries in the period under consideration
4. The customers are handled by 10 salespersons
5. Each enquiry is assumed to correspond to one product
6. Postal Pincode has been taken as the proxy for the location of the construction site for which the enquiry is being generated, and need not be identical to the actual address of the customer
7. Minimal AI assistance has been used in this project, particularly for the following:
   * Mockarooo to generate customer names
   * ChatGPT to check for mathematical errors and inconsistencies, and assist in handling Excel formulae and DAX queries. The DAX queries have been uploaded in this folder.

# Enquiry Analytics
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

### Enquiry Analytics Report:
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
4. Monthly Enquiries: A variation of the number of enquiries by month is presented here. The visual can be drilled down to the day level
5. 

# Limitations
1. Due to synthetic nature of the data, some numbers can appear to be dramatic. For instance, the visual named "Top 10 Customers" contains 4 customers tied at 60 enquiries.
2. Price analytics has been omitted for simplicity
3. Product level data has not been considered in this analysis, and quantities have been omitted for simplicity
4. Pincodes do not show a reliable geographical spread as multiple enquiries can get concentrated in one bubble

However, the data is fictional and constructed according to the best of my knowledge using human judgement without assistance from other individuals or AI to create the numbers or simulate real-world constraints and chaos. 
