# Working Files for the Project
The mechanism and logic behind creation and integrity of the data for this project are presented in this section.

## Employee Data
A total of 23 employees have been involved in the transactions pertaining to this analysis. The employees have been assigned a unique ID, and the names have been inspired by popular movie characters.  

The data pertaining to employees are as presented in this table:  
| Employee Division | Excel Sheet | Remarks |
|---|---|---|
|Sales Team| Sales Employees.xlsx | Names and IDs of 10 employees in the Sales team |
| Procurement Team | Procurement Employees.xlsx | Names and IDs of 8 employees in the Procurement team |
| Fulfilment Team | Fulfilment Employees.xlsx | Names and IDs of 5 employees in the Fulfilment team |

## Generating Customers
Using Mockaroo API, a total of 500 unique customers was generated along with their gender. A unique customer ID (cust_ID) was generated for each customer.  

However, real data is messy and riddled with duplicates. Thus some names were selected at random and made to duplicate their preceding rows. Some names have been duplicated thrice, although most duplicates appeared twice per name. To preserve uniqueness outside the cust_ID, phone numbers were assumed to be unique for each customer. These unique phone numbers (with +91 code) were generated using randbetween() function, and correcting for duplicates.  

The salespersons were assigned customers based on the order of their employee ID, applied as per the cust_ID one below the other. Thus, 500 customers were mapped to 10 salespersons.  

Another constraint was that real businesses can be conducted as per B2B (Business-to-Business) or B2C (Business-to-Customer) modes. Thus the customers had to be classified as Individuals (B2C) and Firms (B2B). The classification was assumed as follows:
| Customer Type | Composition | Number of Customers |
|---|---|---|
| Individual | 62% |	310 |
| Firm	| 38% |	190 |

190 customers were picked at random and assigned "Firm (B2B)" status. However, firms 
