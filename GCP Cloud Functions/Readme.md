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

![image](./Sscreenshots/003.PNG)

2.2. Select  **+Enable APIs and Services**.

2.3. Enable the following APIs:

- Cloud Functions API
- Cloud SQL Admin API
- Secret Manager API
- Cloud Build API

## Step 3: Create Source Bucket

3.1. Go to [Cloud Storage Console.](https://console.cloud.google.com/storage)

3.2. 

