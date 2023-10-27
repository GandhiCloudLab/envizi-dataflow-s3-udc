# Envizi Learning Journey - Dataflow - Sending UDC excel to S3

This tutorial explains about how to setup Envizi Dataflow automation for sending Universal Data Connector excel template to Envizi via AWS S3 bucket for the data Ingestion / Integration.

#### Authors
[Jeya Gandhi Rajan M](https://community.ibm.com/community/user/envirintel/people/jeya-gandhi-rajan-m1), [Indira Kalagara](https://community.ibm.com/community/user/envirintel/people/indira-kumari-kalagara1)

## Pre-Requisites

The only Pre-Requisites for this tutorial is to have IBM Envizi ESG Suite access with Administrator  privileges.

## Steps

Here are the steps that you need to follow.

### 1. Create Data Service for S3

Need to create a Data Service for S3 bucket.

1. Open the Data Services by clicking  `Admin > Data flow Automation`

![](/labs/images/img-11.png)

The Data services page is opened.

2. Click on `Add New Service`

![](/labs/images/img-12.png)

3. Enter the following.

- Type : Amazon S3
- Onwer : Envizi
- Name : Enter any value

4. Click on `Save`

![](/labs/images/img-13.png)

The Data service is created.

5. Open the Data Services by clicking  `Actions > Manage Connections`

![](/labs/images/img-14.png)

The `Manage Connections` page of the data service is opened.

![](/labs/images/img-15.png)

6. Note down the values of the following in a text file
- Bucket 
- Folder
- UserName
- Access Key
- Secret Access Key


### 2. Create Data Pipeline

Need to create Data pipeline to download udc files from S3 bucket and push to Envizi for data ingestion. 

1. Open the Data Pipeline by clicking  `Data pipelines` from the top links.

![](/labs/images/img-16.png)

The Data pipelines page is displayed.

2. Click on `Add New Pipeline`

![](/labs/images/img-17.png)

3. Enter the following.

- Name : Enter any value
- Target System : Accounts
- FileName Pattern : Regex pattern need to be given. For Accounts related data the file starts with POC. ex: ^POC.*\.xlsx
- Data Source : Give the S3 data source that we created before
- Data Transformer : None. (No need of any transformation.)

4. Click on `Save`

![](/labs/images/img-18.png)

The Data pipeline is created.

![](/labs/images/img-19.png)


### 3. Sending UDC excel to S3

Lets use the sample python script [main.py](https://github.com/GandhiCloudLab/envizi-dataflow-sending-udc-excel-to-s3-blog/blob/main/python/main.py) to push the [data.xlsx](https://github.com/GandhiCloudLab/envizi-dataflow-sending-udc-excel-to-s3-blog/blob/main/python/data.xlsx) file into S3 now. 

1. Download the `main.py` and `data.xlsx` files into a folder.

2. Update the `Location` column in the `data.xlsx` with the some existing location in your envizi environment.

Here is the sample content of the excel file.

![](/labs/images/img-21.png)


3. Open the linux/mac terminal window and goto folder where you downloaded the `main.py` file.

4. Instal the `boto3` for python if it is not available in your system.
```
python -m pip install boto3
```

5. Run the below command with your S3 Data service values.
```
export s3_BUCKET_NAME=envizi-client-dataservice-us-prod
export s3_FOLDER_NAME=client_9608cd600af647
export s3_ACCESS_KEY=AKIxxxxxxxxxxxxxxx
export s3_SECRET_KEY=axhHxxxxxxxxxxxxxx

```
6. Run the below command to push the file to S3
```
python main.py
```

you may get the output like this..
```
S3Handler  ...
 ENVIZI_S3_AWS_BUCKET_NAME : envizi-client-dataservice-us-prod
 ENVIZI_S3_AWS_FOLDER_NAME : client_9608cd600af647
output/results-10122023-110535-725742/POC Account Setup and Data Load_G1_20231012-110543.xlsx is uploaded to envizi-client-dataservice-us-prod  : client_9608cd600af647/POC Account Setup and Data Load_G1_20231012-110543.xlsx
2023-10-12 11:05:45,747 - INFO:127.0.0.1 - - [12/Oct/2023 11:05:45] "POST /api/turbo/query HTTP/1.1" 200 -
```

The envizi should have processed your file now.

7. Goto file delivery status screen by Clicking on `File Delivery Status`

You can see the status of your file and notice that it has got processed.

![](/labs/images/img-20.png)


8. You can see the account got created and available in the Org Hierarchy.

![](/labs/images/img-22.png)
![](/labs/images/001-modules.png)


## Summary

As an Envizi user, you might have understood about how to create data service for S3, create date pipeline and send UDC excel template to Envizi via S3 bucket.


## Next steps

The next step is to Get a closer look at IBM Envizi and how it can help accelerate your ESG strategy.

Start your 14-day IBM Envizi ESG Suite trial
https://www.ibm.com/account/reg/us-en/signup?formid=urx-51938

Request your personalized IBM Envizi demo
https://www.ibm.com/account/reg/us-en/signup?formid=DEMO-envizi