# access-db-01

```sql
/* Step1: 005_Customer left join 006_All_YTD_Data */

SELECT		 * 
INTO 		007_Customer_All_fields
FROM		005_Customer AS a_5 
RIGHT JOIN  006_All_YTD_Data AS a_6 
ON 			a_5.[Outlet Key] = a_6.[Outlet Key];

/* Step2: Reformat Customer Table */

SELECT  a_0.[Date], 
        a_7.[a_5_Outlet Key] as [Outlet Key], 
	a_7.Outlet, a_7.[Credit to Outlet Key(CTO)] as [CTO], 
	a_7.Agent, a_7.[Legacy Key Account Key], 
	a_7.[Customer Per Rate Schedule], 
	a_7.[Distributer Identifier], 
	a_7.Cust_Type, 
	a_7.[Cust Group - per CCL] as [Product Grouping], 
	a_7.[Teradata Material Key] as [Material#], 
	a_7.[Volume CY Date Range] as [Volume],
	a_7.[Off Inv Disc CMA CY Date Range]+a_7.[Off Inv Disc CTM CY Date Range]+a_7.[Off Invoice Disc CY Date Range] AS [CMA],
	a_7.[On Invoice NSI CY Date Range]

INTO 	008_Customer_Clean_Table
FROM 	007_Customer_All_fields AS a_7, 
		000_Date_Lookup AS a_0
WHERE   (((a_0.DayNum)=[a_7].[Calendar Day of Year Number]));
```
