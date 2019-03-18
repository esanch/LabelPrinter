# LabelPrinter
Print Sales|Purchase|Work orders with up-to-date information such as ItemCode, Part Number, Description, etc. Built using Teklynx's Label Designer CODESOFT, program works hand in hand with Company's Database Files to produce relevant labels based on provided information.


## Table of contents
* [Features](#features)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Installing](#installing)
  * [Running](#running)
    * [Sales](#sales)
    * [Purchasing](#purchasing)
    * [Work](#work)
* [Built With](#built-with)
* [Troubleshooting](troubleshooting)
* [Authors](#authors)
* [Copyright and License](#copyright-and-license)


## Features
Few things you can do using CODESOFT's Label Printer:
* View Purchase|Sales|Work order label previews based on Order Number and other required parameters
* Print individual labels per Items in a given Purchase|Sales|Work order
  * *Quantity of labels (for Purchase|Sales) is dependent on quantity of each item in the order
* View Item values that make up an order


## Getting Started

### Prerequisites
* CODESOFT [[Demo]](https://www.teklynx.com/en/products/request-demo?product=CODESOFT)


### Installing 
1. Click on [Download as Zip](https://dev.azure.com/UnitedBakeryEquipment/_git/Label%20Printer?path=%2F&version=GBmaster) to retrieve necessary Orders files<br />
2. Depending on the type of order you are working on (Purchase|Sales|Work) select the correct folder to view the label printer<br />


### Running

#### Sales
*\*Refer to [Installing](#installing) prior to running program\**
1. Once program files are downloaded, double-click and run **sales.Xmf** file <br />
	*\*An interactive dialog window will appear*<br />
2. On the interactive window locate and click the box right of **"Order Number:"**<br />
	*\*This will allow user to select a sales order based on the dropdown menu of orders*<br />
  *\*A user may also choose to manually input the sales order number they are trying to reference*
3. Once the preview label loads in the pane above move on to selecting an ItemCode <br />
4. Locate and click the button to the right of **"ItemCode:"** <br />
  *\*A second blue-green interactive dialog window will appear which the user will be able to select an Item Code*<br />
5. From the drop down the user must select an Item Code they wish to print a label for<br />
  *\*Once Item Code is selected click **"OK"** to return to the previous window*<br />
6. Click **"Print"** once you are are content with the values in the preview pane to print the provided label <br />
7. Complete steps 4-6 for each additonal item you wish to print from an order <br />
	*\*Follow from steps 2-6 to change the order number you are working on* <br />
8. To close the program simply click the **"X"** on the top right corner of the dialog box<br />


#### Purchasing
*\*Refer to [Installing](#installing) prior to running program\**
1. Once program files are downloaded, double-click and run **purchase.Xmf** file <br />
	*\*An interactive dialog window will appear*<br />
2. On the interactive window locate and click the box right of **"Order Number:"**<br />
	*\*This will allow user to select a sales order based on the dropdown menu of orders*<br />
  *\*A user may also choose to manually input the purchase order number they are trying to reference*
3. Once the preview label loads in the pane above move on to selecting an ItemCode & Job <br />
4. Locate and click the button to the right of **"ItemCode | Job:"** <br />
  *\*A second blue interactive dialog window will appear which the user will be able to select an Item Code and a Job ID*<br />
5. From the drop down the user must select the parameters they wish to print a label for<br />
  *\*Once the Item Code AND Job are selected click **"OK"** to return to the previous window*<br />
6. Click **"Print"** once you are are content with the values in the preview pane to print the provided label <br />
7. Complete steps 4-6 for each additonal Item/Job you wish to print from an order <br />
	*\*Follow from steps 2-6 to change the order number you are working on* <br />
8. To close the program simply click the **"X"** on the top right corner of the dialog box<br />


#### Work
*\*Refer to [Installing](#installing) prior to running program\**
1. Once program files are downloaded, double-click and run **workOrders.Xmf** file <br />
	*\*An interactive dialog window will appear*<br />
2. On the interactive window locate and click the box right of **"Work Order:"**<br />
	*\*This will allow user to select a sales order based on the dropdown menu of orders*<br />
  *\*A user may also choose to manually input the work order number they are trying to reference*
3. Once the preview label loads in the pane above move on to selecting an ItemCode & PartNumber <br />
4. Locate and click the button to the right of **"ItemCode | PartNumber:"** <br />
  *\*A second orange interactive dialog window will appear which the user will be able to select an Item Code and a Part No*<br />
5. From the drop down the user must select the parameters they wish to print a label for<br />
  *\*Once the Item Code AND Part No are selected click **"OK"** to return to the previous window*<br />
6. Click **"Print"** once you are are content with the values in the preview pane to print the provided label <br />
7. Complete steps 4-6 for each additonal Item/PartNumber you wish to print from an order <br />
	*\*Follow from steps 2-6 to change the order number you are working on* <br />
8. To close the program simply click the **"X"** on the top right corner of the dialog box<br />


## Built With
* Label Designer - [CODESOFT](https://www.teklynx.com/en/products/label-design-solutions/codesoft)
#### For usage on
* [Brady IP300 Printer](https://www.bradyid.com/retired-printers/IP-printer?Ntt=ip%20printer)


## Troubleshooting
*\*In the event an error arises ensure the following parameters are met*
* Labels are correctly retrieving data from dat8121 & QODBC databases
	 1. Open the **Purchase**|**SalesOrders**|**WorkOrder** **.lab** file corresponding to the Order type you are working on through CODESOFT 
	 2. All sub-Tables in **Purchase**|**SalesOrders**|**WorkOrder** **.lab** **Table lookup** point to **dat8121** as the selected data source under **Selct a data source**
	 2. Ensure **Table lookup** and **When printed** have the same value in the paranthesis to the right
	 	- (6) for **SalesOrders.lab** & **Purchase.lab** and (7) for **WorkOrder.lab** <br />
	 3. See [SQL queries](#queries) to ensure all values have the correct query input under **SQL \[SQL Query Builder\]**


### Queries
* [Sales Order](#squery) Query
* [Purchase](#pquery) Query
* [Work Order](#wquery) Query

#### SQuery
* DescTable:
	```
	SELECT [lbl_SalesOrder].[Description] FROM [lbl_SalesOrder] WHERE 
	[lbl_SalesOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_SalesOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefNoPrint]
	```
* ItemTable
	```
	SELECT DISTINCT [lbl_SalesOrder].[ItemCode] FROM [lbl_SalesOrder] WHERE 
	[lbl_SalesOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefNoPrint] 
	ORDER BY ItemCode
	```
* JobTable
	```
	SELECT [lbl_SalesOrder].[PONumber] FROM [lbl_SalesOrder] WHERE 
	[lbl_SalesOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_SalesOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefNoPrint]
	```
* PartNoTable
	```
	SELECT [lbl_SalesOrder].[PartNumber] FROM [lbl_SalesOrder] WHERE 
	[lbl_SalesOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_SalesOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefNoPrint]
	```
* QuantityTable
	```
	SELECT [lbl_SalesOrder].[Quantity] FROM [lbl_SalesOrder] WHERE 
	[lbl_SalesOrder].[PartNumber] = APPLICATION.DOCUMENT.[PartNoPrint] AND 
	[lbl_SalesOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_SalesOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefNoPrint]
	```
* RefTable
	```
	SELECT DISTINCT [RefNumber] FROM [lbl_SalesOrder] 
	ORDER BY RefNumber DESC
	```
	
#### PQuery 
* DescTable
	```
	SELECT [lbl_PurchaseOrder].[Description] FROM [lbl_PurchaseOrder] WHERE 
	[lbl_PurchaseOrder].[PartNumber] = APPLICATION.DOCUMENT.[PartPrint] AND 
	[lbl_PurchaseOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_PurchaseOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefPrint]
	```
* ItemTable
	```
	SELECT DISTINCT [lbl_PurchaseOrder].[ItemCode] FROM [lbl_PurchaseOrder] WHERE 
	[lbl_PurchaseOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefPrint] 
	ORDER BY ItemCode DESC
	```
* JobTable
	```
	SELECT [lbl_PurchaseOrder].[Job] FROM [lbl_PurchaseOrder] WHERE 
	[lbl_PurchaseOrder].[PartNumber] = APPLICATION.DOCUMENT.[PartPrint] AND 
	[lbl_PurchaseOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_PurchaseOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefPrint]
	```
* PartTable
	```
	SELECT [lbl_PurchaseOrder].[PartNumber] FROM [lbl_PurchaseOrder] WHERE 
	[lbl_PurchaseOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_PurchaseOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefPrint]
	```
* QuantityTable
	```
	SELECT [lbl_PurchaseOrder].[Quantity] FROM [lbl_PurchaseOrder] WHERE 
	[lbl_PurchaseOrder].[Job] = APPLICATION.DOCUMENT.[JobPrint] AND 
	[lbl_PurchaseOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_PurchaseOrder].[RefNumber] = APPLICATION.DOCUMENT.[RefPrint]
	```
* RefTable
	```
	SELECT DISTINCT [RefNumber] FROM [lbl_PurchaseOrder] 
	ORDER BY RefNumber DESC
	```

#### WQuery
* DescTable
	```
	SELECT [lbl_WorkOrder].[Description] FROM [lbl_WorkOrder] WHERE 
	[lbl_WorkOrder].[PartNum] = APPLICATION.DOCUMENT.[PartPrint] AND 
	[lbl_WorkOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_WorkOrder].[WorkOrder] = APPLICATION.DOCUMENT.[WorkOrderPrint]
	```
* ItemTable
	```
	SELECT DISTINCT [lbl_WorkOrder].[ItemCode] FROM [lbl_WorkOrder] WHERE 
	[lbl_WorkOrder].[WorkOrder] = APPLICATION.DOCUMENT.[WorkOrderPrint] 
	ORDER BY ItemCode
	```
* JobTable
	```
	SELECT [lbl_WorkOrder].[WorkOrderDetail] FROM [lbl_WorkOrder] WHERE 
	[lbl_WorkOrder].[PartNum] = APPLICATION.DOCUMENT.[PartPrint] AND 
	[lbl_WorkOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_WorkOrder].[WorkOrder] = APPLICATION.DOCUMENT.[WorkOrderPrint]
	```
* LocTable
	```
	SELECT [lbl_WorkOrder].[Location] FROM [lbl_WorkOrder] WHERE 
	[lbl_WorkOrder].[PartNum] = APPLICATION.DOCUMENT.[PartPrint] AND 
	[lbl_WorkOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_WorkOrder].[WorkOrder] = APPLICATION.DOCUMENT.[WorkOrderPrint]
	```
* PartTable
	```
	SELECT DISTINCT [lbl_WorkOrder].[PartNum] FROM [lbl_WorkOrder] WHERE 
	[lbl_WorkOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND
	[lbl_WorkOrder].[WorkOrder] = APPLICATION.DOCUMENT.[WorkOrderPrint] 
	ORDER BY PartNum
	```
* QtyTable
	```
	SELECT [lbl_WorkOrder].[Qty] FROM [lbl_WorkOrder] WHERE 
	[lbl_WorkOrder].[PartNum] = APPLICATION.DOCUMENT.[PartPrint] AND 
	[lbl_WorkOrder].[ItemCode] = APPLICATION.DOCUMENT.[ItemPrint] AND 
	[lbl_WorkOrder].[WorkOrder] = APPLICATION.DOCUMENT.[WorkOrderPrint]
	```
* WorkOrderTable
	```
	SELECT DISTINCT TOP (1000) [WorkOrder] FROM [lbl_WorkOrder] .
	ORDER BY WorkOrder DESC
	```

## Authors
**Elizabeth Earl**
* [Stack Overflow](https://stackoverflow.com/users/10267094/e-earl)
* [GitHub](https://github.com/esanch/)


## Copyright and License
Code and documentation rights reserved 2019 [Elizabeth Earl](mailto:elizabeth.earl@ubeusa.com)

Code released under supervision of [United Bakery Equipment](http://ubeusa.com/)
