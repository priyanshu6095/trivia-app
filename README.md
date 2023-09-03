# Repository README

## Version 1.0

**Note**: The exercises in this course will have an associated charge in your AWS account. In this exercise, you will create the following resources:

- AWS Cloud9 environment
- Amazon Simple Storage Service (Amazon S3) bucket
- Amazon API Gateway REST API
- Amazon DynamoDB table
- AWS Step Functions state machine
- AWS Lambda functions

The final exercise includes instructions to delete all the resources that you create in the exercises.

**Please familiarize yourself with AWS pricing for the following services:**
- AWS Cloud9 Pricing
- Amazon S3 Pricing
- Amazon API Gateway Pricing
- Amazon DynamoDB Pricing
- AWS Step Functions Pricing
- AWS Lambda Pricing

Also, be aware of the AWS Free Tier.

---

### Exercise: Setting Up Your Development Environment

In a production environment, you would typically create a customer-managed policy in AWS Identity and Access Management (IAM) for precise control over your policies. This policy would then be attached to a new user, and you would log in to the AWS Management Console with that user. However, because you are working in an exercise environment, those steps were omitted.

#### Task 1: Creating an AWS Cloud9 Environment and Downloading the Application

1. Choose Services and search for Cloud9 in the Oregon (US-West-2) Region.
2. Create an environment named "trivia-app."
3. Download the application using the following commands:

```shell
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/DEV-AWS-MO-DevOps-C1/downloads/trivia-app.zip -O ~/trivia-app.zip
unzip -o ~/trivia-app.zip
```

#### Task 2: Creating the Backend Infrastructure

1. In the trivia-app folder, use AWS SAM to build the template.yaml file:

```shell
cd trivia-app
sam build
sam deploy --guided
```

2. During the SAM guided deployment:
   - For Stack Name, enter "trivia-app."
   - For AWS Region, press Enter.
   - Confirm changes before deploy, press Enter.
   - Allow SAM CLI IAM role creation, press Enter.
   - Save arguments to configuration file, press Enter.

You should receive confirmation that the stack was created successfully.

3. Copy the Websocket Value from the Outputs table in the terminal output.

#### Task 3: Testing the Frontend on AWS Cloud9

1. Update the trivia-app/front-end-react/src/config.js file with the Websocket endpoint.
2. Set the Node version to v16 (codename: Gallium):

```shell
nvm install lts/gallium
nvm alias default lts/gallium
```

3. Change to the front-end-react directory and install NPM dependencies:

```shell
cd front-end-react/
npm install
npm run start
```

4. Preview the application in the AWS Cloud9 environment.

#### Task 4: Deploying the Frontend to an S3 Bucket

1. Create a uniquely named Amazon S3 bucket:

```shell
aws s3 mb s3://<your_initials><numbers>-trivia-app-bucket/
npm run build
aws s3 sync --acl public-read build s3://<your_initials><numbers>-trivia-app-bucket/
```

2. View the application hosted on your bucket using the URL, which should look like:

```
https://<your_initials><numbers>-trivia-app-bucket.s3.amazonaws.com/index.html
```

#### Task 5: Putting the Application Under Source Control

1. Choose AWS Cloud9 > Go To Your Dashboard in the menu bar.
2. Search for CodeCommit in Services and create a repository named "trivia-app."
3. Configure Git with your name and email address:

```shell
git config --global user.name "<REPLACE_WITH_YOUR_NAME>"
git config --global user.email <REPLACE_WITH_YOUR_EMAIL>
```

4. Initialize your repository, create a branch, commit, and push the code:

```shell
cd ~/environment/trivia-app/
git init
git checkout -b main
git add .
git commit -m "initial commit"
git remote add origin codecommit://trivia-app
git push origin main
```

This README provides step-by-step instructions for setting up your development environment, deploying backend and frontend resources, and putting the application under source control.

For any questions or feedback, please contact us at [AWS Support](https://support.aws.amazon.com/#/contacts/aws-training).

© 2021 Amazon Web Services, Inc. or its affiliates. All rights reserved. This work may not be reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited. All trademarks are the property of their respective owners.# trivia-app
