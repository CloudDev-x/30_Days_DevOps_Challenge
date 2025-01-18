# NBA Game Day Notifications / Sports Alerts System

## Overview
This project is a real-time alert system that sends NBA game day scores to users via SMS/Email. It leverages AWS services (SNS, Lambda, EventBridge) and NBA APIs, demonstrating efficient cloud-based notification mechanisms.

---

## Features
- Fetches live NBA game scores via SportsData.io API.
- Sends formatted updates via SNS (SMS/Email).
- Automates updates using EventBridge.
- Ensures security with least-privilege IAM roles.

---

## Prerequisites
- SportsData.io API Key and account.
- AWS account with basic AWS/Python knowledge.

---

## Technologies
- **AWS Services:** SNS, Lambda, EventBridge.
- **External API:** SportsData.io (NBA).
- **Programming:** Python 3.x.

---

## Project Structure
```
game-day-notifications/
├── src/
│   ├── gd_notifications.py          # Lambda function code
├── policies/
│   ├── gd_sns_policy.json           # SNS permissions
│   ├── gd_eventbridge_policy.json   # EventBridge permissions
│   └── gd_lambda_policy.json        # Lambda permissions
├── .gitignore
└── README.md                        # Documentation
```



