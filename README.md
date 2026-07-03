# Smart Partner API Usage Monitoring with Slack, Jira & Gmail Alerts

This workflow monitors partner API usage in real time and triggers alerts based on usage thresholds. It validates incoming data, calculates usage percentage and routes actions using a Switch node. Slack notifications are sent at 80%, Jira tickets are created at 90% and critical alerts (Email + Jira + Slack) are triggered at 100%.

### Quick Implementation Steps

1. Import the workflow into n8n.
2. Configure the Webhook node and test with sample data.
3. Add credentials for Slack, Jira and Gmail.
4. Update Slack channel ID, Jira project and email recipient.
5. Activate the workflow.
6. Send test payloads to verify all alert levels.

## What This Workflow Does

This workflow helps monitor partner API usage automatically and ensures timely alerts when usage reaches defined thresholds. It starts by receiving usage data through a webhook, validating the payload and calculating the usage percentage based on quota and consumption values.

Once calculated, the workflow routes the data using a Switch node:

- **80% usage** → Sends an early warning Slack notification.
- **90% usage** → Creates a Jira ticket and sends a Slack notification.
- **100% usage** → Sends a critical email alert, creates a Jira ticket and posts a Slack notification.

This approach provides better visibility, enables timely action and helps prevent service disruption.

## Who's This For?

- SaaS platforms with API-based billing
- DevOps and Engineering teams
- Product and Platform teams
- Customer Success managers
- Businesses managing partner integrations

## Requirements

- **n8n** (Cloud or self-hosted). If you don't have an instance yet, you can deploy one using our **[n8n Automation Solutions](https://www.weblineindia.com/n8n-automation/)**.
- Slack account with API access
- Jira Software Cloud account
- Gmail account (OAuth configured in n8n)
- API or system capable of sending usage data via webhook

## How It Works & Setup Guide

### 1. Webhook Setup

Configure the **Incoming Partner Usage Data** node.

- Accept **POST** requests.
- Required payload fields:
  - `partner_id`
  - `partner_name`
  - `quota`
  - `consumed`
  - `timestamp`

### 2. Validate Payload

The workflow validates incoming requests for:

- Missing required fields
- Invalid values
- Incorrect data formats

### 3. Calculate Usage

The workflow calculates API usage percentage using the provided quota and consumed values.

If usage is below **80%**, execution stops without sending notifications.

### 4. Switch Routing

Based on calculated usage:

- **80%** → Slack notification
- **90%** → Jira ticket + Slack notification
- **100%** → Gmail alert + Jira ticket + Slack notification

### 5. Configure Integrations

Configure the following nodes:

- **Slack** → Set the destination channel ID.
- **Jira** → Configure project and issue type.
- **Gmail** → Specify recipient email address.

### 6. Test Workflow

Send sample webhook payloads representing each threshold and verify that:

- Slack notifications are delivered.
- Jira issues are created.
- Critical emails are sent.

### 7. Activate

Enable the workflow after successful testing.

## How To Customize

- **Webhook Node** → Change endpoint path or add authentication.
- **Validation Node** → Validate additional fields such as plan or account owner.
- **Calculation Node** → Modify threshold calculations.
- **Switch Node** → Adjust percentage ranges.
- **Slack Node** → Customize notification messages and channels.
- **Jira Node** → Modify issue templates and priorities.
- **Gmail Node** → Update recipients, subject lines and email templates.

## Add-ons & Enhancements

- Alert deduplication to avoid repeated notifications
- Store usage history in Google Sheets or a database
- Notify multiple email recipients
- Integrate with CRM or billing platforms
- Add cooldown periods or rate limiting
- Enrich partner information using external APIs

## Use Case Examples

- Monitor API usage for SaaS partners.
- Prevent service disruptions before quota exhaustion.
- Automatically trigger internal review workflows.
- Notify account managers for upgrade opportunities.
- Improve operational visibility across engineering and customer success teams.

## Troubleshooting Guide

| Issue | Possible Cause | Solution |
|--------|----------------|----------|
| Workflow not triggering | Webhook not called | Verify webhook URL and HTTP method |
| Invalid payload error | Missing required fields | Ensure all required fields are included |
| Slack message not sent | Incorrect channel or credentials | Reconfigure Slack credentials and channel |
| Jira ticket not created | Invalid project or API issue | Verify Jira credentials and project settings |
| Email not sent | Gmail OAuth issue | Reconnect Gmail account |
| Incorrect usage percentage | Invalid data format | Ensure quota and consumed values are numeric |

## Need Help?

If you need help customizing this workflow, integrating it with your partner management platform, or extending it with advanced API monitoring, reporting, and intelligent alerting, our **WeblineIndia** team is ready to assist.

Explore our **[Process Automation Solutions](https://www.weblineindia.com/process-automation-solutions.html)** or connect with our **[n8n workflow development experts](https://www.weblineindia.com/n8n-automation/)** to build, customize, and scale your business automation with confidence.
