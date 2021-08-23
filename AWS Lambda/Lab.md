# Welcome to the AWS Lambda for Azure Functions user's tutorial (GUI edition)

To get the most from this tutorial, you must know how to hoost  on Azure. In this tutorial you will build an EKS cluster on AWS, deploy worker nodes and install a simple guestbook application. You will be using AWS' `us-west-2` region to deploy your EKS cluster. 

This is a free lab that takes 30 minutes to complete. Make sure you terminate all the services at the end of this lab. 

## Overview

In this tutorial, you will create a simple web application. You will first build a static web app that renders "Hello World." Then you will learn how to add functionality to the web app so the text that displays is based on a custom input you provide.
This tutorial will walk you through the steps to create this sample web application. You will learn to:
- Create a web app
- Connect the web app to a serverless back-end
- Add interactivity to your web app with an API and a database

## Application Architecture

![Architecture Diagram](./png/001.png)

## **Step 0: Before You Start**

You will need to make sure you have the following components installed and set up before you start with Amazon EKS:

- **AWS Account –** Sign up for a free AWS account [here.](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
- **Required IAM permissions** – The IAM security principal that you're using must have permissions to work with AWS Lambda IAM roles and service linked roles. You must complete all steps in this guide as the same user.
  
## **Step 1: Create Web App**
