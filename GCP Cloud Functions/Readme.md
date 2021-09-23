# GCP Cloud Functions for Azure Functions user's tutorial (GUI edition)

To get the most from this tutorial, you must know how to deploy applications using Azure Funcitons. 

This is a free lab that takes 30 minutes to complete. Make sure you terminate all the services at the end of this lab. 

## Overview

In this tutorial, you will create a simple library processing system. When a new text document is added to the source bucket, your function will add this to the books collection in the database.
This tutorial will walk you through the steps to create this sample processing system. You will learn to:
- Create a serverless back-end function
- Add interactivity to your function with storage and database
- Add security to the function operations

## Application Architecture

![Architecture Diagram](./screenshots/001.PNG)

- **Cloud Storage -** We will use the [AWS Identity and Access Management (IAM) service](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) to securely give our services the required permissions to interact with each other.
- **Cloud Functions -** All of your static web content, including HTML, CSS, JavaScript, images and other files, will be hosted by [AWS Amplify.](https://docs.aws.amazon.com/amplify/latest/userguide/welcome.html)
- **Secrets Manager -** We will use [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) to create a RESTful API that will allow us to make calls to our Lambda function from a web client.
- **Cloud SQL -** You will use the compute service [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html), to create serverless functions, writing a small piece of code in Python to add interactivity to your web page.

## Step 0: Before You Start

You will need to make sure you have the following components installed and set up before you start with Amazon EKS:

- **GCP Account –** Sign up for a free GCP account [here.](https://cloud.google.com/free/docs/gcp-free-tier)

## Step 1: Select a Project

If you haven’t created a project yet, create a project. 

Select the project you have created from the dropdown list

![image](./Screenshots/002.png)

## Step 2: Enable APIs

2.1. For each service you use, you need to ensure the Google cloud APIs are enabled. From the cloud console, go to the API and Services page.

![image](./Screenshots/003.PNG)

2.2. Select  **+Enable APIs and Services**.

2.3. Enable the following APIs:

- Cloud Functions API
- Cloud SQL Admin API
- Secret Manager API
- Cloud Build API
- Compute Engine API

## Step 3: Create Source Bucket

3.1. Go to [Cloud Storage Console.](https://console.cloud.google.com/storage)

3.2. Select **+Create Bucket**.

3.3. Name your bucket - *docs\<yournameinitials\>*, for e.g. *docsdj*.

3.4. For **Location type**, select *Region*. In the **Location** drop down options, select `us-west3 (Salt Lake City)`.

3.5. Select *Standard* for **Choose default storage class for your data**.

3.6. Click the **Create** button.

## Step 4: Create the Library Database

### 4.1. Create Cloud SQL Instance

4.1.1. Go to [Cloud SQL Console.](https://console.cloud.google.com/sql)

4.1.2. Select **Create Instance**.

4.1.3. Select **Choose MYSQL**.

4.1.4. For **Instance ID**, type *myinstance*.

4.1.5. Add a **Passowrd** to access your database with secured privileges.

4.1.6. Select `us-west3 (Salt Lake City)` for **Region**.

4.1.7. Select *Single Zone* for **Zonal availability**.

4.1.8. Select **Show Configuration Options** under Customize your instance.

4.1.9. Select *Shared core* as your **Machine Type**.

4.1.10. Under Storage, select *10 GB* as **Storage capacity**. *Uncheck* **Enable automatic storage increases**.

4.1.11. Under Backups, *uncheck* **Automate backups** and **Enable point-in-time recovery**.

4.1.12. Click **CREATE INSTANCE**.

4.1.13. **Copy and save** the **Connection name** under the Overview tab (you will need it in Step 5).

### 4.2. Create Books Table in the Library Database

4.2.1. Setup **Cloud Shell**. Click on the **Activate Cloud Shell** icon on the top right corner in GCP Console.

![image](./Screenshots/004.PNG)

4.2.2. Use the below command in cloud shell to connect to your database instance created in Step 4.1. Click **Authorize** when prompted.

~~~
gcloud sql connect myinstance --user=root
~~~

4.2.3. When prompted, type the password you created in the Step 4.1.5. and press the *Enter* key.

4.2.4. Use the below SQL commands to create a database named *library* and a table named *books*.

~~~
CREATE DATABASE library;
USE library;
CREATE TABLE books (title VARCHAR(100));
INSERT into books (title) VALUES ("Digital Transformation 2020");
~~~

4.2.5. To verify the insertion of the first record from the last command, use the below SQL command

~~~
select * from books;
~~~

You should see 1 row set as shown below

![image](./Screenshots/005.PNG)

## Step 5: Add Security for Database Connection

5.1. Go to [Secret Manager.](https://console.cloud.google.com/security/secret-manager)

5.1. Select **+ Create Secret**.

5.2. For **Name**, type *dbconnectionname*. In the **Secret Value** field, type the *\<Database Connection Name\>* saved in Step 4.1.13. Click **CREATE SECRET**.

5.3. Go back to the Secret Manager Parent Page. Repeat Steps 5.1. and 5.2. to create 2 additional secrets.
- Secret Name: *dbuser* and Secret Value: *root*
- Secret Name: *dbpassword* and Secret Value: *\<type the password you created in the Step 4.1.5.>*

## Step 6: Create Serverless Function

### 6.1. Create a function.

6.1.1. Go to [Cloud Functions Console.](https://console.cloud.google.com/functions)

6.1.2. Select **Create Function**.

6.1.3. For **Function name**, type *librarysys*.

6.1.4. Select `us-west3` as the **Region**.

6.1.5. Select *Cloud Storage* as the **Trigger Type**.

6.1.6. Select *Finalize/Create* as the **Event Type**.

6.1.7. Click on **BROWSE** to select the source bucket you create in Step 3.

6.1.8. Click on **SAVE**.

### 6.2. Add





