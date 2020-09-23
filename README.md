# CloudBank Solution Repo: Zero2Data
## A CloudBank Solution Repo on staging data on the cloud and making it available through an API

### Overview

Your research team needs to access a simple tabular dataset in a computer program. 
This repo walks you through publishing the data on the cloud and building a programmatic interface
to get small subsets of that data using a very simple query protocol. 


[Here is a link](https://docs.google.com/presentation/d/1LVCK0Szvvyhhgzuvk1U19P8XL9qaAKOuDXEJcYeAVTA/edit?usp=sharing)
to a presentation on this topic from FOSS4G-NA 2019.


This CloudBank solution repository uses three sequential tutorial subfolders.

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


* **Why?** Science advances when data availability is not an obstacle; but often it *is*. We built this open tool 
for data publication as a set of templates to overcome this obstacle. There are many additional motivations that 
touch on more specifics of data-driven research from writing good Data Management Plans -- and executing on them --
to supporting team collaboration to demonstrating data democratization to reproducibility. 


* **How?** We create a publication pattern built from real *need-driven* use cases. 
Our model for self-publishing datasets presumes domain expertise applied to the data; an informed
(but not dictatorial) frame of mind. The procedural depends in particulars on the AWS cloud technology stack;
but with an open design that would easily translate to other clouds. Three provided Python code templates
do the work where the second in the sequence, the API translator, requires the bulk of the effort. 
We also provide a test dataset and of course the procedural. From there it is a matter of messaging
availability and in the tradition of open source seeing how community trial and adoption goes.


* **What?** We prototype a system on the AWS public cloud with two culmination points. First the 
table access API returns simple query results (HTML or JSON). Second we build a *composition API* that 
delivers a higher-level derived results: Speed and dispersion for the group of individuals described
by the data table. The derived result API makes use of the table access API. We address sub-topics 
in passing including documentation, data security, API design, registration of the resource, 
complexity, cost, source citation, discovery and obsolescence. 


### Extended narrative


It can be tempting to try and build extensive customization into a data access API. 
We suggest making the data access API as simple as possible.  
This avoids anticipating future use and *does not prevent* building more sophisticated APIs. 
The idea is to layer APIs to create higher-level data products without compromising a simple base API.
We will refer to this as API *composition*: Once a dataset is emplaced we are 
free to write a second data service (and a third, and a fourth, ...) built upon the first.
Higher-level APIs might for example make use of other resources. 


As an example consider prediction of juvenile salmon survival rates in a river. 
This would be a science or operational goal for a project that begins with 
hatchery release data as a 'Zero2Data candidate' simple source table). 
The survival prediction service might work from hypothetical conditions informed by past 
data across many additional resources; for example precipitation and stream gauge data, 
turbidity sensor data, water temperature records, bird counts, 
sport fishing catch records, water chemistry field data and so on. 
Philosophically the idea is to build the salmon prediction service 
on infrastructure that uses but is independent of the Zero2Data hatchery data solution. 


The solution given here begins with a tabular dataset (CSV file).
Here is the [(back-story link)](https://en.wikipedia.org/wiki/Amboseli_Baboon_Research_Project) 
for this dataset. The CSV file has one million rows by four columns with headers **`indiv, time, x, y`**.


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
