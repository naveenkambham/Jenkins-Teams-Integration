# Jenkins and Microsoft Teams Integration
This repository provides a guide and configuration files for integrating Jenkins with Microsoft Teams to streamline communication around your CI/CD pipeline. With this setup, your team can receive real-time notifications in Microsoft Teams channels on build status, deployment progress, and other critical updates, enabling faster responses and improved collaboration.

## Features
* Automated Build Notifications: Receive instant notifications on build statuses (success, failure, etc.) directly in Teams channels.
* Customizable Alerts: Tailor notifications to include build details, commit messages, author information, or any other relevant data.
* Simple Setup with Webhooks: Uses Microsoft Teams webhooks for easy setup and configuration.

## Getting Started
Follow these steps to set up Jenkins and Microsoft Teams integration:

1. Go to the Teams channel where you want to receive notifications and select Workflows.
2. Create a new workflow with the following steps:
    * select workflow type/template to "Post to a channel when a webhook request is received" and click Next
    * select/confirm Team Name and Teams Channel details and click Add Workflow
    * Newly created Workflow can be viewed and edited under Workflows menu inside Teams app. 
    * Copy the Webhook URL 
3. Configure Jenkins:
    * In Jenkins, go to Manage Jenkins > Configure System -> Plugins -> Install new plugin named "Flexible Publish".
    * Go to Post-build Actions and Add "Flexbile Publish".
    * Flexible Publish -> Configure Conditional Actions to ("Success" in the Worst and Best Status cases)
    * Flexible Publish  -> Configure Action with Webhook URL and Set the mode to "POST" and select Yes for Ignore SSL errors
         * Click Advanced inside Action to include the payload and configure the settings 
         * Authenticate: None
         * Use system properties: No
         * Headers -> Accept : NOT_SET
         * Headers -> Content-Type: APPLICATION_JSON
         * Body -> Pass build params to URL : No
         * Request body: Refer to JSON file in the project folder
         * File Upload: No 
    * Repeat the same steps for Build Failure cases
    * Click Save and Trigger the Jenkins Build 
    
