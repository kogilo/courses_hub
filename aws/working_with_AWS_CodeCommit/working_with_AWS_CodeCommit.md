
# https://www.qwiklabs.com/catalog

# Working with AWS CodeCommit
## Overview
* **AWS Codecommit**:-
  - is highly scalable, managed source control that hosts private Git repositories.
  - it stores your data in Amazon S3 & Amazon DynamoDB giving your repositories **high scalability, availability, & durability**.
  - simply, create a repository to store your code.
  - no hardware to provision & scale or software to install, configure, and operate.
## Objective of this lab:
* practice with AWS CodeCommit, part of AWS Developer Tools.
* create a code repository in AWS CodeCommit.
* create a local repository on a Linux instance in EC2
* after you create local repo, you will make some change to it.
* then you will synchronize (commit) your changes to the **AWS CodeCommit repository**.

## Task 1: Create an AWS CodeCommit Repository
* 3. In the AWS Management Console, on the Services menu, click Codecommit.
* 4. Click the **Create repository**
* 5. On the ** Create repository page, configure:
  - **Repository name**: My-Repo
  - **Description**: `My first repository`
  - Click `Create`
* An empty repository called `My-Repo` will be created in AWS CodeCommit. Connection details will be displayed

## Task 2: Connect to your EC2 Instance
* An EC2 has been created for you as part of the lab. In this task, you will connect to this instance.
