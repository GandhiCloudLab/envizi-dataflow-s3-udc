# Envizi - Dataflow automation with S3 and Universal Data Connector

This article explains the step by step instruction about how to send Universal Data Connector excel to Envizi via S3 Data Service.

- Universal Data Connector excel file for Accounts and Data can be processed.


## 1. Create Data Service for S3

Need to create a Data Service for S3 bucket.

1. Open the Data Services by clicking  `Admin > Data flow Automation`

<img src="images/img-11.png">

The Data services page is opened.

2. Click on `Add New Service`

<img src="images/img-12.png">

3. Enter the following.

- Type : Amazon S3
- Onwer : Envizi
- Name : Enter any value

4. Click on `Save`

<img src="images/img-13.png">

The Data service is created.

5. Open the Data Services by clicking  `Actions > Manage Connections`

<img src="images/img-14.png">

The `Manage Connections` page of the data service is opened.

<img src="images/img-15.png">

6. Note down the values of the following in a text file
- Bucket 
- Folder
- UserName
- Access Key
- Secret Access Key


## 2. Create Data Pipeline

Need to create Data pipeline to download udc files from S3 bucket and push to Envizi for data ingestion. 

1. Open the Data Pipeline by clicking  `Data pipelines` from the top links.

<img src="images/img-16.png">

The Data pipelines page is displayed.

2. Click on `Add New Pipeline`

<img src="images/img-17.png">

3. Enter the following.

- Name : Enter any value
- Target System : Accounts
- FileName Pattern : Regex pattern need to be given. For Accounts related data the file starts with POC. ex: ^POC.*\.xlsx
- Data Source : Give the S3 data source that we created before
- Data Transformer : None. (No need of any transformation.)

4. Click on `Save`

<img src="images/img-18.png">

The Data pipeline is created.

<img src="images/img-19.png">


## 3. Push a UDC excel to S3

1. You can push the UDC excel to S3 using the above collected info (Bucket, access key, etc) from the S3 Data Services.

The envizi should have processed your file.

2. Goto file delivery status screen by Clicking on `File Delivery Status`

<img src="images/img-19.png">

You can see the status of your file.

<img src="images/img-20.png">
