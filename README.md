# Scheduled-Cron-Job-Via-Lambda-Cloudwatch

# Step 1: Create a Lambda function

- Open the Lambda Console
- Choose Create function, Author from Scratch
- Under Basic Information, Enter the Function Name which specifies our Lambda code.
- Runtime choose, Python 3.9
 
 Choose Create function (Lambda function will be created using the Basic Lambda role)
Under the Function Code, write the following code. This function is used to hit the specified URL.

```sh
import json
from urllib.request import urlopen
def lambda_handler(event, context):
   # open a connection to a URL using urlopen
    webUrl = urlopen("https://database.talimarfinancial.com/CronJobFCI/sendRemainderBorrober") #Specify the URL to hit
    #get the result code and print it
    print ("result code: " + str(webUrl.getcode()))
```

(Reference for Code: https://www.guru99.com/accessing-internet-data-with-python.html)

- Make sure your URL is with https
- Choose Deploy
- Choose Test 
- In the Configure test event dialog box, choose Create new test event.
- Enter an Event name. Then, choose Create.
- Choose Test to run the function.
- You got 200

You you get the timeout got the Configurationthen then General configuration and edit the timeout to 1:00 min 

# Step 2: Create a cloudwatch event, specifying the CRON expression.(https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/Create-CloudWatch-Events-Scheduled-Rule.html)

- Open the Cloudwatch Console
- Choose events, under Navigation Pane and Create Rule      //
- For Event source select Schedule
- Choose Cron Expression and specify the Cron Expression as per your wish
(Reference how to specify CRON Expression: https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html)
- For Targets, Choose Add Target. Choose Lambda function and choose the specified Lambda function for which we need the CRON to run.
- Select configure Details
-Enter the Cloudwatch Name and fill Description if needed.


Click Create Rule.

