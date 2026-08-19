# Data Modelling
The mechanism and logic behind creation and integrity of the data for this project are presented in this section.

## Contents
1. [Background] (#background)
2. [Employee Data] (#employee-data)
3. [Generating Customers] (#generating-customers)
4. [Generating Enquiries] (#generating-enquiries)
5. [Assigning Dates to Enquiries] (#assigning-dates-to-enquiries)
6. [Assigning Product Category to Enquiries] (#assigning-product-category-to-enquiries)
7. [Assigning Pincodes] (#assigning-pincodes)
   * [Assigning Pincodes to Enquiries] (#assigning-pincodes-to-enquiries)
   * [Assigning Pincodes to Customers] (#assigning-pincodes-to-customers)
8. [Conclusion] (#conclusion)

## Background
The project simulates selected aspects of an e-commerce business firm in Chennai, Tamil Nadu, which deals with four product categories namely Cement, AAC Blocks, Steel and Concrete. The data reflect a snapshot of Indian fiscal year 2022-23 (FY23 - April 1, 2022 to March 31, 2023). Therefore local factors like customs, naming conventions and regional Pincodes have been infused into the data.

## Employee Data
A total of 23 employees have been involved in the transactions pertaining to this analysis. The employees have been assigned a unique ID, and the names have been inspired by popular movie characters.  

The data pertaining to employees are as presented in this table:  
| Employee Division | Excel Sheet | Remarks |
|---|---|---|
|Sales Team| Sales Employees.xlsx | Names and IDs of 10 employees in the Sales team |
| Procurement Team | Procurement Employees.xlsx | Names and IDs of 8 employees in the Procurement team |
| Fulfilment Team | Fulfilment Employees.xlsx | Names and IDs of 5 employees in the Fulfilment team |

## Generating Customers
The details of customers can be viewed in the sheet named Customer Master.xlsx. Using Mockaroo API, a total of 500 unique customers was generated along with their gender. A unique customer ID (cust_ID) was assigned to each customer.  

However, real data is messy and riddled with duplicates. Thus some names were selected at random and made to duplicate their preceding rows. Some names have been duplicated thrice, although most duplicates appeared twice per name. To preserve uniqueness outside the cust_ID, phone numbers were assumed to be unique for each customer. These unique phone numbers (with +91 code) were generated using randbetween() function, and corrected for duplicates.  

The salespersons were assigned customers based on the order of their employee ID, applied as per the cust_ID one below the other. Thus, 500 customers were mapped to 10 salespersons.  

Another constraint was that real businesses can be conducted as per B2B (Business-to-Business) or B2C (Business-to-Customer) modes. Thus the customers had to be classified as Individuals (B2C) and Firms (B2B). The classification was assumed as follows:
| Customer Type | Composition | Number of Customers |
|---|---|---|
| Individual | 62% |	310 |
| Firm	| 38% |	190 |

190 customers were picked at random and assigned "Firm (B2B)" status. To add to the authenticity, the second names of these selected customers were edited using the following common names (to resemble construction firms found in Chennai region):
| Firm Suffix | Number of Firms |
| --- | --- |
| Builders	| 33 |
| Homes Pvt Ltd	| 21 |
| Construction	| 57 |
| Constructions	| 24 |
| Builders and Construction	| 2 |
| Homes	| 6 |
| Associates	| 8 |
| Property Construction	| 1 |
| Construction Pvt Ltd	| 10 |
| Groups	| 9 |
| Civil Solutions	| 5 |
| Foundation	| 7 |
| Design and Developers	| 3 |
| Developer	| 4 |  

The rows were split using List.Numbers function in Power Query and the firm names were edited accordingly. Some firm names were again intentionally manipulated to reflect real world messy data (Eg: Samaria Construction and Samaria Constructions).  
The remaining customers were assigned "Individual (B2C)" status.  

## Generating Enquiries
An enquiry is the act of a customer where he/she asks for availability of the product, while specifying his/her preferences and negotiating for his/her limitations. It is the first step in the business transaction.  
To generate enquiries, each customer was allotted a random number of enquiries (between 1 and 60) until a satisfactory mix of regular and infrequent customers was obtained. The total number of enquiries for 500 customers in FY23 added up to 5,944. This number was fixed for upcoming calculations.  

Using List.Numbers function in Power Query, the customers were split into 5,944 rows, and shuffled using rand() function until a satisfactory randomness was obtained. This was then copied to the sheet named Enquiry Master.xlsx, and each enquiry was assigned a unique Enquiry ID. The enquiries were assigned to the salesperson as mapped to the respective customer. 

## Assigning Dates to Enquiries
The next challenge was to assign enquiries to the dates in FY23. A calendar was first created as per the following steps:  
1. A sheet listing dates from April 1, 2022 to March 31, 2023 was prepared in the sheet named Calendar Master.xlsx.
2. Days of the week were mapped automatically to the respective dates to check for Sundays.
3. The following holidays as per the actual calendar were marked on the sheet:

| Date | Day | Holiday |
|---|---|---|
| 14-Apr-22	| Thursday	| Tamil New Year |
| 15-Aug-22	| Monday	| Independence Day |
| 31-Aug-22	| Wednesday	| Vinayakar Chathurthi |
| 04-Oct-22	| Tuesday	| Ayutha Pooja |
| 05-Oct-22	| Wednesday	| Vijaya Dasami |
| 24-Oct-22	| Monday	| Deepavali |
| 16-Jan-23	| Monday	| Pongal |
| 17-Jan-23	| Tuesday	| Pongal |
| 26-Jan-23	| Thursday	| Republic Day |

4. The days between 10-12 December, 2022 were marked as affected by Cyclone Mandous (which had affected normal life in general and construction projects in particular in the city)
5. The remaining days were assigned the status of "Working Days"

The next process was to divide the 5,944 enquiries for 12 months. The steps were as follows:
1. Zero enquiries were assumed and subsequently assigned on Sundays, holidays and the days affected by the cyclone
2. For the remaining days, the business was assumed to have a general rising trend, with intentional dips on some days or seasons.
3. A small dip was assumed in September and October due to festivities and local factors, culminating in a rise in November
4. As the firm was based in Chennai, a dip in construction projects was expected in the Tamil month of Margazhi (December 16, 2022 to January 14, 2023), all the way to the festival of Pongal (January 14-16, 2023). However, the pent up demand was carried to the month of February
5. The enquiries were broken down on a monthly basis to reflect the general rising trend and occasional dips. The enquiries were first assumed to be on average between 494-496 per month, and manually adjusted to reflect these assumptions. The final output is as follows:

|	Month	|	Assigned Enquiries	|
|	------	|	------	|
|	April	|	421	|
|	May	|	457	|
|	June	|	468	|
|	July	|	497	|
|	August	|	570	|
|	September	|	480	|
|	October	|	476	|
|	November	|	566	|
|	December	|	383	|
|	January	|	441	|
|	February	|	566	|
|	March	|	619	|

Now the enquiries had to be assigned to each working day. The logic is as follows:
1. The working days were calculated for every month, and equal enquiries were initially assumed for each working day

|	Month	|	Assigned Enquiries	|	Working Days per Month	|	Per Day Enquiries	|
|	------	|	------	|	------	|	------	|
|	April	|	421	|	21	|	20.04761905	|
|	May	|	457	|	26	|	17.57692308	|
|	June	|	468	|	26	|	18	|
|	July	|	497	|	26	|	19.11538462	|
|	August	|	570	|	25	|	22.8	|
|	September	|	480	|	26	|	18.46153846	|
|	October	|	476	|	23	|	20.69565217	|
|	November	|	566	|	26	|	21.76923077	|
|	December	|	383	|	25	|	15.32	|
|	January	|	441	|	23	|	19.17391304	|
|	February	|	566	|	24	|	23.58333333	|
|	March	|	619	|	27	|	22.92592593	|

2. Consider April. For the 21 working days, Excel randbetween() function was used to assign random enquiries between 14 and 21 for each day, and manually adjusted to get the total of 421. The numbers were also adjusted to ensure the day-level fluctuations were not dramatic.
3. For the other months, a similar approach was followed after adjusting the upper and lower limits of randbetween() function.
4. Thus, the Calendar Master had enquiries attached to each day.
5. The working days were loaded into Power Query, and the rows for each date were split List.Numbers function based on the number of enquiries per day.
6. The repeating dates were pasted to the Enquiry Master sheet, ensuring that each enquiry ID was mapped to only one date.

With this, the dates were assigned to each enquiry.

## Assigning Product Category to Enquiries
The file named Product Master.xlsx lists the names and Item ID of 4 product categories namely Cement, AAC Blocks, Steel and Concrete. These have to be mapped to 5,944 enquiries. The assumption here is that there is only one product per enquiry. Weights for each product category were assumed and the number of enquiries were calculated as follows:  

|	Item ID	|	Item Name	|	Enquiry Volume (%)	|	Total
|	------	|	------	|	------	|	------
|	I01	|	Cement	|	36.98	|	2198
|	I02	|	Steel	|	17.01	|	1011
|	I03	|	AAC Blocks	|	34.02	|	2022
|	I04	|	Concrete	|	12.00	|	713

The products were first distributed to each the month, with more or less the same weights. The values were adjusted to maintain whole numbers, and the final month-wise calculation was as follows:  

|	Month	|	Total	|	Cement	|	Steel	|	AAC Blocks	|	Concrete
|	------	|	------	|	------	|	------	|	------	|	------
|	April	|	421	|	156	|	72	|	142	|	51
|	May	|	457	|	171	|	77	|	154	|	55
|	June	|	468	|	174	|	80	|	159	|	55
|	July	|	497	|	184	|	83	|	171	|	59
|	August	|	570	|	209	|	97	|	194	|	70
|	September	|	480	|	178	|	82	|	163	|	57
|	October	|	476	|	176	|	82	|	162	|	56
|	November	|	566	|	209	|	97	|	192	|	68
|	December	|	383	|	142	|	65	|	130	|	46
|	January	|	441	|	159	|	77	|	152	|	53
|	February	|	566	|	211	|	95	|	192	|	68
|	March	|	619	|	229	|	104	|	211	|	75

The rows for each month were split using List.Numbers function in Power Query, and rows corresponding to each product category were obtained for all months. A random number was assigned to each row using rand() function, and the 5,944 rows were were sorted by month and then by the random number. The sorting process was repeated until a satisfactory level of randomness was observed. The product column was then pasted to the Enquiry Master sheet, with one enquiry ID mapped to one product category.

## Assigning Pincodes
A postal index number code (Pincode) is a six digit number used by the Department of Posts of India to represent locations in the country. In this analysis, the Pincode has been taken as the proxy for addresses for the purpose of simplification. Pincodes have been assigned separately for customers and enquiries. The former corresponds to the customer's/firm's address, while the latter corresponds to the actual construction site. The file named "Pincodes.xlsx" contains the list of Pincodes allotted to both enquiries and customers.

### Assigning Pincodes to Enquiries
To obtain the Pincodes, the file named "TN Pincodes.pdf" was downloaded from the India Post website and loaded into Power Query. Four postal divisions namely Tambaram, Chennai City North, Chennai City South and Chennai City Central were chosen to represent the Chennai region. The enquiries were assumed to be distributed across 45 Pincodes.
Based on my real experience and prevailing trends, weights for the number of enquiries were attached to these postal divisions, and the result was calculated as follows:

|	Division	|	Composition (%)	|	No of Enquiries	|	No of Pincodes	|
|	------	|	------	|	------	|	------	|
|	Tambaram	|	40.02	|	2379	|	18	|
|	Chennai City North	|	16.60	|	987	|	7	|
|	Chennai City South	|	28.36	|	1686	|	12	|
|	Chennai City Central	|	15.01	|	892	|	8	|

The data under the column named "No of Pincodes" was manually adjusted until a satisfactory distribution was obtained. 

Using List.Numbers() function of Power Query, the Divisions were duplicated into the same numbers of rows as the "No of Pincodes" column above. Then, from the "TN Pincodes.pdf" Query mentioned earlier, relevant Pincodes based on actual construction prevalence were selected and pasted next to the table. The number of enquiries were manually adjusted for these locations based on real world trends and limitations until a satisfactory mix was obtained. For instance, Koyambedu had fewer enquiries than the nearby areas of Arumbakkam and Nerkundram because the former is more of a transport hub and while the latter areas had a higher preference of residential and infrastructure projects.  

As an example, the data for "Chennai City North" is presented here:

|	Postal Division	|	Area	|	Pincode	|	No of Enquiries	|
|	------	|	------	|	------	|	------	|
|	Chennai City North	|	Koyambedu S.O	|	600107	|	148	|
|	Chennai City North	|	Nerkundram S.O	|	600107	|	178	|
|	Chennai City North	|	Washermanpet East S.O	|	600021	|	57	|
|	Chennai City North	|	Perambur S.O	|	600011	|	177	|
|	Chennai City North	|	Chintadripet	|	600002	|	88	|
|	Chennai City North	|	Arumbakkam S.O	|	600106	|	187	|
|	Chennai City North	|	Vyasarpadi S.O	|	600039	|	152	|

This data was loaded into Power Query, and the rows were duplicated as per the "No of Enquiries" column using the List.Numbers() function. With this, 5,944 rows were obtained. Using rand() function, a random number was allotted to these rows and then sorted, until a realistic mix was observed. The rows of these Pincodes along with the Area Name was pasted into the Enquiry Master sheet.

### Assigning Pincodes to Customers
Customer addresses were assumed to be spread across 35 Pincodes. The customers were spread across the 4 Postal Divisions mentioned earlier as per the calculation below:

|	Division	|	Composition (%)	|	No of Customers	|	No of Pincodes	|
|	------	|	------	|	------	|	------	|
|	Tambaram	|	40	|	200	|	6	|
|	Chennai City North	|	16	|	80	|	8	|
|	Chennai City South	|	30	|	150	|	12	|
|	Chennai City Central	|	14	|	70	|	9	|

The rows were first split as per "No of Pincodes" in Power Query and the locations were assigned manually from the TN Pincodes file. The rows were split again as per  the "No of Customers" column to obtain 500 rows. These rows were assigned a random number (using rand()) and shuffled until a realistic arrangement was obtained. The area names and pincodes were pasted into the Customer Master sheet.

## Conclusion
A summary of the work done is as follows:
1. A total of 23 employees was assumed for the analysis and distributed across the Sales, Procurement and Fulfilment teams
2. A total of 500 customers were assumed to have been involved in some form on interaction with the business in FY23. Customer names could be duplicate or nearly identical, and they were split between B2B (business-to-business) and B2C (business-to-customer) modes of transaction
3. The customers generated 5,944 enquiries in FY23. Enquiry generation was affected by Sundays, festivals, local customs and other factors affecting customer demand
4. A calendar was allotted to account for day-level distribution of enquiries.
5. Each enquiry corresponded to 1 product category, and the mix was accounted for upto the day-level
6. Pincodes based on the Chennai region were allotted separately to enquiries and customers

Thus, the data for an e-commerce business facing a general rising trend in the number of enquiries for FY23 was constructed. Further details of relationship schemas, codes and queries can be viewed in the folders of the respective reports.

Feel free to contact me for queries and feedback!
