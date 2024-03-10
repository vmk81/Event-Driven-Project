# Event Driven Architecture using Amazon EventBridge, Lambda, SNS and S3.  
## Summary
This Project is to demonstrate how we can build an Event driven architecture using Amazon EventBridge, Lambda,SNS and S3. The Python code for Lambda and the JSON code for the Event Patterns are also provided.  
![Arch-2](https://github.com/vmk81/Event-Driven-Project/assets/157844406/950b09ae-cf91-40b2-a061-42dc821b3624)  

If a file is uploaded to the S3 bucket(PutObject), then the EventBridge will call a Lambda Function which will print an output saying that a new file has been uploaded. This output can be verified in CloudWatch.  
If a file is deleted from the S3 bucket(DeleteObject), then the EventBridge will call an SNS Topic which will send an email to the email address provided in the subscription.

This project will involve the following sections.  

Section 1: Create an S3 bucket.  
Section 2: Create a Lambda Function  
Section 3: Create an SNS Topic  
Section 4: Create Event Buses in EventBridge.  
Section 5: Test the Output  

## Detailed Procedure
### Section 1: Create an S3 bucket and enable Amazon EventBridge.
1. Open the S3 console and click on ‘Create bucket'. Enter a unique bucket name which is my-event-bucket in this case and select the region. Click ‘Next’ and click ‘Create bucket’.  
![1-Create S3](https://github.com/vmk81/Event-Driven-Project/assets/157844406/9d960260-a63d-4e29-858f-8df263f8c272)
2. Navigate to the newly created bucket (my-event-bucket) and click on Properties tab(Red Arrow).Scroll down to Event Notifications and click Edit under Amazon EventBridge. Select the 'On' button(Black Arrow).
![2-S3 EventBridge Enable](https://github.com/vmk81/Event-Driven-Project/assets/157844406/3c36636c-2ff7-41e3-a40a-20d21f1734b3)  

### Section 2: Create a Lambda Function
3. Navigate to Lambda service and click on 'Create function'. Choose 'Author from scratch'. Give a Function name and choose the Runtime as Python 3.12 . Then click on 'Create function' button. 
![5-Create Lambda](https://github.com/vmk81/Event-Driven-Project/assets/157844406/02fa9474-ae9a-4625-a211-9ee00dae376d)  
4. On the following page inside the code section(Red Arrow) and copy/paste the Lambda Function code that will accept the JSON event from the EventBridge.
![6-Create Lambda Add Code](https://github.com/vmk81/Event-Driven-Project/assets/157844406/993c8af2-e6c3-4a10-a62c-0df2547400d3)

### Section 2: Create an SNS Topic and subscription. 
5. Navigate to SNS service and give a name to the topic (Red Arrow) and click on 'Next step' button. Leave all the options as it is and click on 'Create Topic' at the bottom of the page. 
![2-Create SNS Topic](https://github.com/vmk81/Event-Driven-Project/assets/157844406/1a141df0-6a5a-419b-884f-5b30e656356a)
6. On the following page click on 'Create subscription' botton. Choose Email as the protocol and enter the email address that should receive the notifications. Then click 'Create subscription'.
![3-Create SNS Subscription](https://github.com/vmk81/Event-Driven-Project/assets/157844406/0dc3d88e-d88b-4e92-89d6-a93d9a21b09a)

### Section 4: Create Event Buses for Lambda and SNS in EventBridge.  
7. Navigate to the EventBridge service. Select EventBridge Rule and Click on 'Create rule'.Provide the rule name(Red Arrow in the below screenshot). Select 'Rule with an event pattern' option(Black Arrow) under Rule Type.
![7-EventBridgerule for Lambda](https://github.com/vmk81/Event-Driven-Project/assets/157844406/2d0f734b-c8d5-46c3-b3d1-26575e0d1bd1)
8. In the Event pattern section, select 'Custom pattern'(Red Arrow in the below screenshot).Copy the JSON code for object creation and click on 'Next'.  
![8-EventBridgerule for Lambda -2](https://github.com/vmk81/Event-Driven-Project/assets/157844406/d6df9243-98bf-404e-8193-7d0b807537be)
9. On the following page, select 'AWS service' and select Lambda Function as select target. Select the Lambda function that was created in step 3 and then click on 'Next'.Scroll to the bottom and click on 'Create rule' button
![9-EventBridgerule for Lambda -3](https://github.com/vmk81/Event-Driven-Project/assets/157844406/7a93d2b1-3872-4e84-a9dc-917dfe9f1215)
10. Go back to EventBridge Rule page and Click on 'Create rule'.Provide the rule name for SNS(Red Arrow in the below screenshot). In the Event pattern section, select 'Custom pattern'(Black Arrow).Copy the JSON code for object deletion and click on 'Next'.
![10-EventBridgeRule for SNS](https://github.com/vmk81/Event-Driven-Project/assets/157844406/44125be8-dc88-4348-9829-00daaa40c437)  
11. On the following page, select 'AWS service' and select SNS topic as select target. Select the SNS topic that was created in step 5 and then click on 'Next'.Scroll to the bottom and click on 'Create rule' button.  
![11-EventBridgeRule for SNS-2](https://github.com/vmk81/Event-Driven-Project/assets/157844406/d6c24d2f-698a-4dc4-b8e4-eabf19aa76e1)

### Section 5: Test the Output  
12. To test the output for Lambda, we will upload a file to the S3 bucket that was created in step 1. Open a powershell prompt on your desktop and upload a file to the S3 bucket using awscli(Red Arrow in the below screenshot). Go back to the S3 bucket on the console and check if the file got uploaded. Take a note of the time of upload(Black Arrow).
![12-Lambda Testing-1](https://github.com/vmk81/Event-Driven-Project/assets/157844406/7ece0fed-67f5-480f-94ff-ef833ca487b7)
13. Go back to Lambda page and select 'Monitor' tab(Red Arrow in the below screenshot) and click on 'View CloudWatch Logs'. Under Logstreams we can see the latest log stream with the same timestamp (Black Arrow)as the time of upload from step 12. If we open the log stream we can see the print output from our Lambda function(Blue Arrow).
![13-Lambda Testing - 2](https://github.com/vmk81/Event-Driven-Project/assets/157844406/5a40e1db-8fc2-424a-b2da-263c18cc9d61)  
14. To test the output for SNS, we will delete the file from the S3 bucket that was uploaded in step 12. Open a powershell prompt on your desktop and delete the file from the S3 bucket using awscli(Red Arrow in the below screenshot). Go back to the S3 bucket on the console and check if the file got deleted. Log into the email account that was provided in step 6 and in the inbox we can see the email notification from AWS regarding the object deletion(Black Arrow).
![14-SNS Testing -1](https://github.com/vmk81/Event-Driven-Project/assets/157844406/b00f0301-9151-4713-924d-2c3e8bec3b4c)


 



