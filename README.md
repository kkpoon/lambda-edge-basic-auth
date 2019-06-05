# lambda-edge-basic-auth

This is a simple implementation of Basic Authentication in AWS Lambda@Edge for controlling access of CloudFront distribution.

To use this lambda, you have to config as follow

1. Deploy this lambda function in `us-east-1`. The function MUST be deployed in `us-east-1` for lambda@edge.
2. Use the following `AssumeRole` for this lambda execution role
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "lambda.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "edgelambda.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```
3. Publish a version of the lambda
4. In CloudFront, config the distribution **Lambda Function Associations**, set the **CloudFront Event** to **Viewer Request**, set your versioned lambda ARN, and leave **Include Body** unchecked.
