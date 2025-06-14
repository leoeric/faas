# faas

Given a Lambda function that is triggered upon the creation of files in an S3 bucket, answer the following:
1. What is the purpose of the execution role on the Lambda function?
Answer: The execution role is an IAM role assumed by the Lambda function during execution. It defines what AWS resources the function is allowed to access or modify.

2. What is the purpose of the resource-based policy on the Lambda function?
Answer: The resource-based policy allows external services or accounts to invoke the Lambda function.
In this case, because the function is triggered by S3 events, the resource-based policy must allow S3 to invoke the Lambda function.

3. If the function is needed to upload a file into an S3 bucket, describe (i.e no need for the actual policies)
- What is the needed update on the execution role?
Answer: s3:PutObject. Limit this permission to the specific S3 bucket the function writes to.

- What is the new resource-based policy that needs to be added (if any)?
Answer: No new resource-based policy is needed on the Lambda function in this case. The Lambda function is calling S3 — not the other way around. IAM policies are unidirectional: Lambda's permissions to write to S3 are governed by the execution role, not by a policy on the S3 bucket or Lambda function (unless bucket policies or SCPs restrict it). However, if the S3 bucket has a bucket policy, it may need to explicitly allow the Lambda function's IAM role to upload to the bucket (especially if it's private or tightly controlled).
