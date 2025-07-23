<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Fetch Data with AWS Lambda

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-lambda)

**Author:** Abdulrahman Abdulkadir  
**Email:** abdabdulkadir62@gmail.com

---

## Fetch Data with AWS Lambda

![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-lambda_p9thryj2)

---

## Introducing Today's Project!

In this project, I will demonstrate how to fetch data using AWS Lambda. I'm doing this project to learn how serverless functions can retrieve data from services like DynamoDB or external APIs, process it, and return a response efficiently without managing any servers.


### Tools and concepts

Services I used were AWS Lambda and Amazon DynamoDB. Key concepts I learnt include Lambda functions, serverless computing, DynamoDB’s schemaless NoSQL design, permission management with IAM roles and policies, and how to securely connect Lambda to DynamoDB for data retrieval.


### Project reflection

This project took me approximately a few hours to complete. The most challenging part was configuring the correct IAM permissions to allow my Lambda function to access DynamoDB securely. It was most rewarding to successfully fetch and return data using a serverless architecture without managing any servers.


I did this project today to gain hands-on experience with serverless computing and database integration using AWS Lambda and DynamoDB. Yes, the project met my goals by helping me understand how to securely connect these services, manage permissions, and build a scalable data retrieval function.


---

## Project Setup

To set up my project, I created a database using Amazon DynamoDB. The partition key is userid, which means each item in the table is uniquely identified by a user's ID. This allows efficient lookups and ensures that data is organized and retrieved based on individual users.


In my DynamoDB table, I added a new item with a userId of 1, a name of Test User, and an email of [test@example.com](mailto:test@example.com). DynamoDB is schemaless, which means I didn’t need to define the name or email attributes ahead of time. Each item can have its own unique set of attributes, giving me flexibility to store data without a fixed structure.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-lambda_a112c3d5)

### AWS Lambda

AWS Lambda is a serverless compute service that runs code in response to events and automatically manages the underlying infrastructure. I'm using Lambda in this project to fetch data from my DynamoDB table without having to provision or maintain a server, allowing for a more efficient and scalable application.


---

## AWS Lambda Function

My Lambda function has an execution role, which is a set of permissions that allows it to interact with other AWS services. By default, the role grants basic permissions such as writing logs to Amazon CloudWatch. I can also attach additional permissions so the function can read data from DynamoDB or access other required services.


My Lambda function will retrieve a user's data from the UserData table in DynamoDB using the userId provided in the event. It sets up a DynamoDB client, constructs a GetCommand with the userId as the key, and sends the request. If data is found, it returns the user item; if not, it logs that no data was found. If there's an error, it logs and returns the error.


The code uses AWS SDK, which is a collection of tools and libraries that allow developers to interact with AWS services programmatically. My code uses SDK to communicate with DynamoDB, send commands to retrieve data, and handle responses within the Lambda function.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-lambda_a1b2c3d5)

---

## Function Testing

To test whether my Lambda function works, I created a test event in the AWS Lambda console with a JSON object containing a sample userId. The test is written in JSON format, matching the expected input structure for the function. If the test is successful, I'd see the user data retrieved from DynamoDB returned in the response and no error messages in the logs.


The test displayed a 'success' because the Lambda function executed without crashing, but the function's response was actually empty or incorrect because the test event did not provide the userId in the expected format or the userId did not exist in the DynamoDB table. This caused the function to return no data or an unexpected result.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-lambda_u1v2w3x4)

---

## Function Permissions

To resolve the AccessDenied error, I updated my Lambda function’s execution role to include permissions for DynamoDB actions like GetItem and Query because without these permissions, the function cannot access the data it needs from the DynamoDB table.


There were four DynamoDB permission policies I could choose from, but I didn't pick the ones granting full table access or delete permissions because they would give my Lambda function more privileges than necessary. Instead, I followed the principle of least privilege by only allowing the specific actions my function needs, like reading data.


I also didn’t pick policies that allow write or delete actions because my Lambda function only needs to read data from DynamoDB. AmazonDynamoDBReadOnlyAccess was the right choice because it grants the necessary permissions to read data securely without giving the function more access than it requires.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-lambda_3ethryj2)

---

## Final Testing and Reflection

To validate my new permission settings, I ran the Lambda function test again using the same test event. The results were successful because the execution role now had the correct DynamoDB read permissions, allowing the function to access and retrieve data from the table without any access errors.


Web apps are a popular use case of using Lambda and DynamoDB. For example, I could build a serverless backend that handles user profiles, stores data, and responds to user requests without managing servers. This setup can scale automatically and reduce costs while providing fast, reliable data access.




![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-lambda_p9thryj2)

---

## Enahancing Security

For my project extension, I challenged myself to replace my Lambda function’s permission policy with a more restrictive one. This will enhance security by ensuring the function only has the exact permissions it needs to perform its tasks, reducing the risk of unintended access or misuse.


To create the permission policy, I used the JSON policy editor because it gives me full control and flexibility to define precise permissions tailored to my Lambda function’s needs, ensuring it has only the minimum required access for security best practices.


When updating a Lambda function’s permission policies, you could risk accidentally removing necessary permissions, causing the function to fail. I validated that my Lambda function still works by running the same test event after the policy update and confirming it successfully retrieved data from DynamoDB without errors.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-lambda_1qthryj2)

---

---
