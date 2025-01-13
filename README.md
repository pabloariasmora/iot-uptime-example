# IoT Machine Uptime Tracking - AWS CloudFormation Template

## Disclaimer

**IMPORTANT**: This code and configuration are intended for educational purposes and teaching exercises only. They are not designed or optimized for production use. For production environments, additional security measures, error handling, and optimizations would be necessary.

## Overview

This project demonstrates a simple IoT machine uptime tracking system using AWS services. It includes a CloudFormation template that sets up an AWS IoT Core rule, a Lambda function, and a DynamoDB table to process and store machine status data.

## Prerequisites

- An AWS account
- AWS CLI installed and configured
- Basic understanding of AWS services (IoT Core, Lambda, DynamoDB)

## Deployment Instructions

1. Save the CloudFormation template (YAML file) to your local machine.

2. Open the AWS CloudFormation console in your AWS account.

3. Click "Create stack" and choose "With new resources (standard)".

4. Select "Upload a template file" and upload the YAML file you saved.

5. Click "Next" and provide a stack name (e.g., "IoTUptimeTracking").

6. You can leave the `MachineDataTopic` parameter as default or change it if needed.

7. Click through the next steps, acknowledge that the template might create IAM resources, and create the stack.

8. Wait for the stack creation to complete.

## Usage

After the stack is created, you can start sending MQTT messages to the IoT Core topic. The Lambda function will process these messages and update the DynamoDB table.

### MQTT Topic Structure

```
devices/{MachineID}/data
```

Replace `{MachineID}` with your actual machine identifier.

### Example Payloads

Here are some example payloads you can use to test the system:

1. Machine 001 active:
```json
{
  "MachineID": "machine001",
  "Timestamp": 1673820000,
  "D2_Data_N": 870
}
```

Machine 002 inactive:

```json
{
  "MachineID": "machine002",
  "Timestamp": 1673820060,
  "D2_Data_N": 450
}
```

Machine 003 active:

```json
{
  "MachineID": "machine003",
  "Timestamp": 1673820120,
  "D2_Data_N": 1280
}
```

## Sending Test Messages
You can use the AWS IoT Core Test Client to send test messages:

1. Go to the AWS IoT Core console.
2. Navigate to "Test" in the left sidebar.
3. In the "Publish" section, enter the topic (e.g., devices/machine001/data).
4. Paste one of the example payloads into the message body.
5. Click "Publish" to send the message.


## Viewing Results
To see the results:

1. Go to the DynamoDB console.
2. Find the table named "machine-status".
3. Use the "Explore table items" feature to view the stored data.

## Limitations
- This system assumes consistent message delivery and doesn't handle missed messages.
- There's no authentication or authorization implemented for the MQTT messages.
- Error handling is minimal.
- The system doesn't account for time zone differences or daylight saving time changes.
  
Remember, this is a simplified example for learning purposes. A production system would require more robust error handling, security measures, and optimizations.
