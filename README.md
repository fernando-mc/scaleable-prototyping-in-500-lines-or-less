# Serverless Application Prototyping in 500 Lines or Less

## Long Description

In this talk, we'll look at how to rapidly develop application prototypes in the cloud. We'll review how to spin up a few sample applications inside of Amazon Web Services using the Serverless Framework to abstract away inner workings of services we'd otherwise have to configure more manually.

In this process, we'll see how a combination of managed services, libraries, and 3rd party tools can build a web application that collects, user-generated content and makes it immediately searchable - all in under 500 lines of user-written code.

We'll look at how to build a prototype with a "Code Budget" with the intention of not spending more time on a particular area of development if at all possible. This will allow us to get out a Minimum Viable Product or MVP out quickly and leave us time to collect and iterate on user-feedback.


## Session Outline

- Who am I/What do I do? (1 min)
- What are we trying to do? (1 min)
    - Focus on how to rapidly prototype application ideas
    - Using managed services, libraries, and 3rd party tools as much as possible
    - Doing as little work as possible as quickly as possible
- What are we building? (2 min)
    - A website that collects user-submitted data about pay rates in tech and then makes it immediately searchable
    - Sneak-peak at full architecture diagram and the final product
    - Remember 500 lines of code or less!

- Reviewing Our Tools (4 min)
    - Note: This is a high-level architecture looking at different parts, more detail as we build things later.
    - AWS Services
        - AWS Lambda - Running our code
        - API Gateway - Creating an HTTP API endpoint
        - Amazon S3 - Storing and hosting our website files 
        - DynamoDB - Durable NoSQL storage for our data 
        - AWS Systems Manager Parameter Store - Managing our API keys
    - Serverless Framework
        - Allows us to easily create HTTP APIs and other resources on AWS
        - Manages all the AWS infrastructure of services for us
        - Uses AWS CloudFormation in the background to deploy backend
        - Excellent community of plugins - one to deploy our frontend
    - Algolia Search
        - Indexes data for search
        - Libraries to build UI components for search
    - Semantic UI
        - Quick Frontend UI
        - Credit to another who helped with the current UI
    - Google reCAPTCHA
        - Spam blocking

- The "Code Budget" (3 min)
    - What is a code budget?
        - A limit on the amount of code we'll write by hand
        - Not the same idea as optimizing our code to a few brilliant 1-liners
        - This is a lazy, non-optimized 500 lines of code
    - Why have it?
        - Keep ourselves limited to a very minimal prototype
        - Theoretically limit time we spend on the process
    - What we're going to spend our 500 hand-written lines of code
        - Frontend (~60%)
        - Backend (~20%)
        - Infrastructure (~8%)
        - Dependency management (~2%)

- How do we build it? (1 min)
    - Walk through the development process
    - Use some code snippets
    - Lots of visuals of the architecture
    - Review how things work together

- Assumptions about the environment (1 min)
    - Should have all these installed/configured:
        - Python 3
        - node and npm
        - Setup an AWS Account and admin user with the AWS CLI (Not Shown)
        - `npm install serverless -g` for Serverless Framework
        - Algolia Account and API Keys
        - Google reCAPTCHA and API Keys

- Create the Serverless Framework project (1 min)
    - Create a `serverless.yml` file
    - Add the basic information about the project
        - Uses AWS, uses Python 3.7

- Create a DynamoDB Table to store data (1 min)
    - Add a resource in `serverless.yml` for the DynamoDB Table
    - Deploy the serverless application `sls deploy`
        - Show screenshot/demo of table in AWS
    - Show master visual with DynamoDB no longer greyed out

- Create API to handle user-submissions (6 min)
    - Write the AWS Lambda Function to process data:
        - New python file with a little code
        - Function accepts/validates inputs
        - Sends them over to the DynamoDB table
    - Configure new Serverless Framework service 
        - Reference new Python file
        - Describe some API configuration
    - Deploy it all
    - Test API with Postman, look at DynamoDB to see data
    - Show master visual with API/Lambda no longer greyed out too

- Create a Frontend that can send data to the API (2 min)
    - Semantic UI, JavaScript/HTML/CSS
    - API Endpoint to send data to
    - Test locally to send data to the API
    - Check DynamoDB that it works after submitting data
    - Show master visual with Frontend no longer greyed out but in the wrong place

- Deploy the frontend files to Amazon S3 and configure static site hosting (2 min)
    - Install `serverless-finch` plugin for the Serverless Framework
    - Configure the plugin with an Amazon S3 bucket
    - Deploy the files to the bucket and visit our new live website

- Setting up our API keys for use (3 min)
    - Get all our API Keys
    - Explain SSM Parameter store
        - Stores secrets, can call it in code with proper permissions to get secrets at runtime
    - Load secrets into SSM Parameter Store
    - Serverless Framework integrates with it
    - Add config for secrets in `serverless.yml`

- Adding Search (3 min)
    - On the Backend
        - Create an Algolia Index
        - Updating our Lambda Function to add data to Algolia
        - Use the Algolia Python library
        - Use the API Keys in SSM Parameter Store
        - Add a new entry and see data in the Algolia console
    - On the Frontend
        - Pre-built JavaScript UI Components 
        - Options for popular JS Frameworks
        - Styling the search results 
    - Redeploying our site and seeing the results

- Adding Spam Protection with reCAPTCHA (2 min)
    - Add Google reCAPTCHA to the frontend with a form field
    - Adding reCAPTCHA check to the backend with a check in the Lambda Function
    - Redeploy both again

- Voilia. A fully functional prototype ready for user feedback and iteration.

- Core principles to use with your ideas (2 min)
    - Keep it simple
    - Don't fret the styles
        - These add up fast as I learned from V2 of this project
        - Show V2 of this project with a line count of Styles
    - Don't tune for performance until you need to
        - This infrastructure could scale up to:
            - 50k searches/mo 
            - 10k records
        - For pennies or less (without a custom domain)
    - It can scale automatically to support millions of searches if needed
    - This sort of prototype gives you the flexibility to fail, iterate, and scale as needed

- Links to code for this project and my information
- Questions? (5 minutes)

## Audience Take-Aways

The audience should feel empowered to leverage several AWS cloud services, the Serverless Framework, and other resources to start to prototype on their own applications. From this talk, they should feel comfortable exploring:

- The AWS Service Catalog
- The Serverless Framework
- Algolia

## Notes For the Program Committee

I'd be interested in doing this either as a workshop or a talk or both. I'm happy with a shorter/longer format with some notice so I can prepare it.