# CloudBank Solution Repo: Zero2Data
## A CloudBank Solution Repo 
### Create a test API
### Stage data on the cloud with an API

### Overview

Imagine: Your team needs to access a simple tabular dataset in a computer program. 
This **CloudBank Solution** walks you through publishing the data on the cloud and building a programmatic interface
with a simple query protocol. 


[Here is a link](https://docs.google.com/presentation/d/1LVCK0Szvvyhhgzuvk1U19P8XL9qaAKOuDXEJcYeAVTA/edit?usp=sharing)
to a presentation on this topic from FOSS4G-NA 2019.


This CloudBank solution repository uses four sequential tutorial subfolders.

0. Create a very simple test case
1. Publish a table
2. Build an API
3. Create a client


### Slightly longer summary

- publish the table
  - Secure and configure a cloud account (working example uses AWS)
  - Organize a `.csv` tabular data file to publish
  - Push the data into a cloud database-as-a-service (AWS DynamoDB table)
- build an application programming interface (API)
  - Associate a serverless API service (AWS Lambda with API Gateway)
  - Attach a stable URL to this service (AWS Elastic IP)
- write and test a `client` of the service


### Motivation


* **Why?** Data availability should not be an obstacle to research. 
We try and illustrate a data resource using the public cloud. 
There are a lot of applications of the idea; from de-coupling data sources from data use, to 
building successful Data Management Plans, to supporting 
team collaboration, supporting data democratization, demonstrating reproducibility, 
and data provenance that extends beyond a project life span. 


* **How?** We'll use the AWS cloud technology stack; with an open design that easily translates to other cloud
platforms (GCP, Azure, etcetera). The main idea is to store the data in a table and set up a serverless
task that receives a data query and replies with data.


* **What?** The 
table access API will return query results (HTML or JSON). 


### Philosophical

We advocate for making the base-level API as simple as possible.  
This is a means of avoiding use bias but it *does not prevent* building more sophisticated APIs. 
A *composition API* can delivers higher-level derived results. 
Higher-level APIs might for example make use of other resources. 


#### Example

Consider prediction of juvenile salmon survival rates in a river. 
This would be a science or operational goal for a project that begins with 
hatchery release data as a 'Zero2Data candidate' simple source table). 
The survival prediction service might work from hypothetical conditions informed by past 
data across many additional resources; for example precipitation and stream gauge data, 
turbidity sensor data, water temperature records, bird counts, 
sport fishing catch records, water chemistry field data and so on. 
Philosophically the idea is to build the salmon prediction service 
on infrastructure that uses but is independent of the Zero2Data hatchery data solution. 


### Amboseli Baboons

The solution given here begins with a tabular dataset (CSV file).
Here is the [(back-story link)](https://en.wikipedia.org/wiki/Amboseli_Baboon_Research_Project). 
The CSV file has one million rows by four columns with headers **`indiv, time, x, y`**.


Each row is a relative location for an individual (in meters).   
Locations were recorded
every two seconds for 26 individuals within a larger *congress* of baboons over the course of one day.
The individual identifiers are 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 18, 20, 
21, 23, 24, 25, 31, 33, 35 and 38.


Procedure outline: 


- Set up an AWS account; select a working **Region** on AWS, ensure DynamoDB is enabled in that region
- In DynamoDB set up an appropriate table; and note the endpoint URL
- On your local machine: Install the `boto3` Python package (the AWS interface library)
- Use `DynamoDB_load.py` to push the data to the DynamoDB table


The above steps are the first phase of three in this the process (one hour to complete).  
This time estimate does not include setting up an AWS account and learning how to manage it.  


The second part of the three-step process builds the data access interface or API 
using the AWS serverless 'Lambda' service. (Serverless means it is easy to set up
and *service* is a generic term meaning *thing you can do on the cloud*.)


The third part of the process is to write a Client that tests your service of course. 

Once parts one and two are complete your example baboon-esque data system will incur a monthly cost. 
Our estimate is $300 for five years. We suggest publishing the details of your service
that you plan to own and operate as a GitHub repository like this one.  

You may wish to respond to an API call that gives no arguments with a docstring. 
