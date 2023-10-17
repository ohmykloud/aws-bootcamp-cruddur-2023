- [Week 0 — Billing and Architecture](#week-0-billing-and-architecture)
   * [My AWS Journey with Andrew](#my-aws-journey-with-andrew)
   * [Pre-Requisites  ](#pre-requisites)
   * [Week-0 Live Session ](#week-0-live-session)
   * [Tasks Completed in Week-0](#tasks-completed-in-week-0)
      + [Install AWS CLI](#install-aws-cli)
      + [Create a new User and Generate AWS Credentials](#create-a-new-user-and-generate-aws-credentials)
      + [Set Env Vars](#set-env-vars)
      + [Check that the AWS CLI is working and you are the expected user](#check-that-the-aws-cli-is-working-and-you-are-the-expected-user)
   * [Recreate Conceptual Diagram ](#recreate-conceptual-diagram)
   * [Conceptual Diagram](#conceptual-diagram)

<!-- TOC end -->

<!-- TOC --><a name="week-0-billing-and-architecture"></a>
# Week 0 — Billing and Architecture
<!-- TOC --><a name="my-aws-journey-with-andrew"></a>
## My AWS Journey with Andrew
This journal consists of the tasks completed in week-0 of AWS Free Bootcamp 2023 organized by Andrew Brown and his Team. In this week, we started with setting up the accounts (aws, gitpod, gihub) that are required before the start of ‘Cruddur Project’. 

<!-- TOC --><a name="pre-requisites"></a>
## Pre-Requisites  
Before beginning with Week-0 we should have these following accounts : 
- Personal AWS account. 
- Gitpod account.  
- Lucid Charts account. 
- GitHub account. 

<!-- TOC --><a name="week-0-live-session"></a>
## Week-0 Live Session 
So, there was a Live Session conducted by the AWS Bootcamp organizer Andrew Brown with the guest lecturers – Shala Warner, Chris Williams and Margaret Veltierra. They are the experts of AWS cloud also known as Cloud Heroes. It was really an amazing Live session where all the lecturers were interacting with each other, was kind of ‘real-time feel’ session.  
***What did we Learn in this Live Session ?***
This was mainly focused on ***Billing and Architecture***
- We learnt how to understand the client’s requirements,  how to segregate tasks and gather the requirements for the project. 
- Different architectures – monolithic and microservice architecture. 
- Introduction to AWS console, Gitpod console, GitHub repositories.  
- Understanding about Conceptual, Logical and Physical Diagrams. 
- Got to knot about TOGAF Architecture.
- C4 models. 
- How to create diagrams in Lucid Charts. 
- Hands on example for My Diagram. 
<!-- TOC --><a name="tasks-completed-in-week-0"></a>
## Tasks Completed in Week-0
**1. Created IAM User, Role and MFA**
![IAM](/_docs/assets/002.jpg)

![](/_docs/assets/003.jpg)
So, it is very easy to create a IAM User and set MFA (Multi Factor Authentication) to it. I followed the below given steps to create this :
- Login as a **root user** into AWS account.
- Search for **IAM service** and go to **Users**.
- **Create a new User** by giving the appropriate **(Admin)** permissions.
  After that to set MFA you can go to particular **User -> Security Credentials -> Enable MFA**.
- Fill the required details and **Scan QR code** from the authentication app in your mobile. (Here you **need to install authentication application in your mobile** to connect it with your IAM User).
- **Enter two MFA Codes** when asked and your MFA is set.

*** 1.Creating IAM Role***
- From IAM click on **Roles -> Create role**.
- Choose **Entity Type** as per your project, I personally chose **AWS Services for EC2 Use case.**
- Added permission policy as **Security Audit**.
- Then give **role name** and **Tags** and click on **Create role**. 

**Error Faced after creating IAM user, role**
It does not gives you access to create billing from IAM User account.

**How to solve?** 
When it displays the error message in that only you can find how to to troubleshoot that error. In this case you have to allow permission for billing configuration access from your root account.
**Enable manage concole access** from security credentials of that IAM User.

**2.Installeed AWS CLI in Gtpod.**

<!-- TOC --><a name="install-aws-cli"></a>
### Install AWS CLI

- We are going to install the AWS CLI when our Gitpod enviroment lanuches.
- We are are going to set AWS CLI to use partial autoprompt mode to make it easier to debug CLI commands.
- The bash commands we are using are the same as the [AWS CLI Install Instructions]https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

By follwoing Andrews's **"Required homework"** video it became so easy specially for beginner level students to undersatnd and install and set AWS CLI on Gitpod. 


![](/_docs/assets/010.jpg)
![](/_docs/assets/011.jpg)
![](/_docs/assets/012.jpg)

There were some most used commands like ```aws configure``` : to set AWS credentials; ```aws sts get-caller-identity``` : for viewing the AWS Account Identity and so on...

Update our `.gitpod.yml` to include the following task.

```sh
tasks:
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init: |
      cd /workspace
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      cd $THEIA_WORKSPACE_ROOT
```

We'll also run these commands indivually to perform the install manually

<!-- TOC --><a name="create-a-new-user-and-generate-aws-credentials"></a>
### Create a new User and Generate AWS Credentials

- Go to (IAM Users Console](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/users) andrew create a new user
- `Enable console access` for the user
- Create a new `Admin` Group and apply `AdministratorAccess`
- Create the user and go find and click into the user
- Click on `Security Credentials` and `Create Access Key`
- Choose AWS CLI Access
- Download the CSV with the credentials

<!-- TOC --><a name="set-env-vars"></a>
### Set Env Vars

We will set these credentials for the current bash terminal
```
export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION=us-east-1
```

We'll tell Gitpod to remember these credentials if we relaunch our workspaces
```
gp env AWS_ACCESS_KEY_ID=""
gp env AWS_SECRET_ACCESS_KEY=""
gp env AWS_DEFAULT_REGION=us-east-1
```


![](/_docs/assets/013.jpg)

<!-- TOC --><a name="check-that-the-aws-cli-is-working-and-you-are-the-expected-user"></a>
### Check that the AWS CLI is working and you are the expected user

```sh
aws sts get-caller-identity
```

You should see something like this:
```json
{
    "UserId": "AIFBZRJIQN2ONP4ETEST",
    "Account": "6556023400000",
    "Arn": "arn:aws:iam::655602346534:user/alexiscloud"
}
```
<!-- TOC --><a name="recreate-conceptual-diagram"></a>
## Recreate Conceptual Diagram 
![Logical Architectual Diagram](/_docs/assets/aws%20diagram-AWS%20Bootcamp%20Logical%20Diagram.svg)


<!-- TOC --><a name="conceptual-diagram"></a>
##  Conceptual Diagram
![ Conceptual Diagram](/_docs/assets/aws%20diagram-Cruddur%20-%20Conceptual%20Diagram.drawio.svg)