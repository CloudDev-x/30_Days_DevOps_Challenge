# Build a Real-Time NBA Game Notification System with Event-Driven Architecture

Creating a real-time notification system for NBA game updates can be a rewarding project that combines cloud computing with sports enthusiasm. This guide will walk you through building a solution that fetches live NBA scores and sends notifications via SMS or email using AWS services like SNS, Lambda, and EventBridge.

---

## Project Overview

This project leverages AWS and the NBA Game API (SportsData.io) to deliver real-time game updates. Subscribed users can receive score notifications via SMS or email, showcasing the capabilities of cloud-based workflows and automation.

---

## Prerequisites

Before starting, ensure you have:

- A SportsData.io API key and account.
- An AWS account with basic AWS and Python knowledge.

---

## Technologies Used

- **Cloud Provider**: AWS
- **Core Services**: SNS, Lambda, EventBridge
- **External API**: NBA Game API (SportsData.io)
- **Programming Language**: Python 3.x

---

## Project Structure

```plaintext
game-day-notifications/
├── src/
│   ├── __init__.py              # Package initializer
│   ├── gd_notifications.py      # Main Lambda function code
├── gd_sns_policy.json           # SNS publishing permissions policy
├── .gitignore                   # Git ignore file
└── README.md                    # Project documentation
```

---

## Step-by-Step Guide

### Step 1: Clone the Repository

Start by cloning the project repository:
```bash
git clone https://github.com/ifeanyiro9/game-day-notifications.git
cd game-day-notifications
```

### Step 2: Create an SNS Topic

1. Open the AWS Management Console and navigate to SNS.
2. Click **Create Topic** and select **Standard**.
3. Name your topic (e.g., `gd_topic`) and note its ARN.
4. Click **Create Topic**.

### Step 3: Add Subscriptions to the SNS Topic

1. Navigate to the **Subscriptions** tab of your topic and click **Create Subscription**.
2. Choose a protocol:
   - For **Email**, enter a valid email address.
   - For **SMS**, enter a phone number in international format (e.g., `+1234567890`).
3. Confirm email subscriptions via the confirmation link sent to your inbox. SMS subscriptions are activated immediately.

### Step 4: Create the SNS Publish Policy

1. Open the IAM service and navigate to **Policies → Create Policy**.
2. Paste the following JSON into the **JSON** tab:
   ```json
   {
       "Statement": [
           {
               "Effect": "Allow",
               "Action": "sns:Publish",
               "Resource": "arn:aws:sns:REGION:ACCOUNT_ID:gd_topic"
           }
       ]
   }
   ```
3. Replace `REGION` and `ACCOUNT_ID` with your AWS region and account ID.
4. Name the policy (e.g., `gd_sns_policy`) and create it.

### Step 5: Create an IAM Role for Lambda

1. In the IAM service, click **Roles → Create Role**.
2. Choose **AWS Service → Lambda**.
3. Attach the following policies:
   - **SNS Publish Policy** (created earlier).
   - **AWSLambdaBasicExecutionRole** (AWS managed policy).
4. Name the role (e.g., `gd_role`) and create it.
5. Save the role ARN for later use.

### Step 6: Deploy the Lambda Function

1. In the Lambda service, click **Create Function → Author from Scratch**.
2. Configure:
   - **Function Name**: `gd_notifications`
   - **Runtime**: Python 3.x
   - **Execution Role**: Select the role created earlier.
3. Add your code:
   - Copy the content of `src/gd_notifications.py` into the inline code editor.
   - Add environment variables:
     - `NBA_API_KEY`: Your NBA API key.
     - `SNS_TOPIC_ARN`: ARN of your SNS topic.
4. Save your function.

### Step 7: Set Up Automation with EventBridge

1. Open EventBridge and navigate to **Rules → Create Rule**.
2. Set **Event Source** to **Schedule** and configure a cron expression for updates (e.g., hourly).
3. Add your Lambda function (`gd_notifications`) as the target and save the rule.

### Step 8: Test the System

1. Open your Lambda function and create a test event.
2. Run the function and check **CloudWatch Logs** for any errors.
3. Verify that notifications are sent to subscribed users.

---

## What You Learned

By following this guide, you’ve learned how to build a real-time notification system using AWS services, secure workflows with least privilege IAM policies, automate workflows with EventBridge, and integrate external APIs into cloud-based applications.




