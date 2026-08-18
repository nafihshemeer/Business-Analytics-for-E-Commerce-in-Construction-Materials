# Working Files for the Project
The mechanism and logic behind creation and integrity of the data for this project are presented in this section.

## Background
The project simulates selected aspects of an e-commerce business firm in Chennai, Tamil Nadu, which deals with four product categories namely Cement, AAC Blocks, Steel and Concrete. The data reflect a snapshot of Indian fiscal year 2022-23 (FY23 - April 1, 2022 to March 31, 2023). Therefore local factors like customs naming conventions and regional Pincodes have been infused into the data.

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

The rows were split using list() function in Power Query and the firm names were edited accordingly. Some firm names were again intentionally manipulated to reflect real world messy data (Eg: Samaria Construction and Samaria Constructions).  
The remaining customers were assigned "Individual (B2C)" status.  

## Generating Enquiries
An enquiry is the act of a customer where he/she asks for availability of the product, while specifying his/her preferences and negotiating for his/her limitations. It is the first step in the business transaction.  
To generate enquiries, each customer was allotted a random number of enquiries (between 1 and 60) until a satisfactory mix of regular and infrequent customers was obtained. The total number of enquiries for 500 customers in FY23 added up to 5,944. This number was fixed for upcoming calculations.  

Using list() function in Power Query, the customers were split into 5,944 rows, and shuffled using rand() function until a satisfactory randomness was obtained. This was then copied to the sheet named Enquiry Master.xlsx, and each enquiry was assigned a unique Enquiry ID. The enquiries were assigned to the salesperson as mapped to the respective customer. 

## Assigning Dates to Enquiries
The next challenge was to assign enquiries to the dates in FY23. The steps are as follows:  
1. A sheet listing dates from April 1, 2022 to March 31, 2023 was prepared in the sheet named Calendar Master.xlsx.
