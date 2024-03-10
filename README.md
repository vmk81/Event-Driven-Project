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
