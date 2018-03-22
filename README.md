# Getting Started with Amazon GuardDuty

This GitHub repository walks you through a scenario covering threat detection and remediation using Amazon GuardDuty. The scenario covers an attack that simulates a few threat vectors which represents just a small sample of the threats that GuardDuty is able to detect. In addition, we look at how to view the GuardDuty findings, how to alert based on the findings, and finally how to remediate findings. The CloudFormation template builds out the assets used to simulate the attacks and the instructions are provided on how to analyze and remediate the findings.

## What is Created?
The CloudFormation template will create the following resources:
  * Three [Amazon EC2](https://aws.amazon.com/ec2/) Instances (all using a t2.micro instance type):
    * Two Instances that contain the name “*Compromised Instance*” 
    * One instance that contains the name “*Malicious Instance*”
  * [AWS IAM Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) For EC2 (which will be attached to two of the instances created)
  * One [Amazon SNS Topic](https://docs.aws.amazon.com/sns/latest/dg/GettingStarted.html) with an subscription for the e-mail address you will enter in the parameters when you run the CloudFormation template
  * Three [AWS CloudWatch Event](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html) rules:
    * Rule named “*GuardDuty-Event-EC2-MaliciousIPCaller*” with two triggers
      * Trigger to publish to the SNS Topic 
      * Trigger to run a Lambda function
    * Rule named “*GuardDuty-Event-IAMUser-InstanceCredentialExfiltration*” with two triggers
      * Trigger to publish to the SNS Topic 
      * Trigger to run a Lambda function
    * Rule named “*GuardDuty-Event-IAMUser-MaliciousIPCaller*” with one trigger
      * Trigger to publish to the SNS Topic 
  * Two [AWS Lambda](https://aws.amazon.com/lambda/) functions
    * Function named “*GuardDuty-Example-Remediation-EC2MaliciousIPCaller*” to remediate the EC2 instance compromise by removing the instance from the current security group and add it to one with no ingress or egress rules
    * Function named “*GuardDuty-Example-Remediation-InstanceCredentialExfiltration*” to remediate the IAM credential compromise by put a revoke policy on the IAM Role from where the credentials were provided.  
  * [AWS Systems Manager Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-paramstore.html) values with the IAM temporary security credentials details.

## Getting started – Just Two Clicks

The CloudFormation template works whether GuardDuty is enabled or not (you just need to indicate the state of GuardDuty in the CloudFormation parameters section). If you would like to enable GuardDuty yourself before running the CloudFormation script then you can follow the instructions below. If you don’t want to enable GuardDuty yourself you can skip to next section titled **Deploy the Solution using AWS CloudFormation**.

It's extremely easy to enable GuardDuty and get stared so it won't take very long to enable it. Also there are no pre-requisites for turning it on and nothing else you need to do. 

Follow these steps to enable GuardDuty
1. **First Click**: Navigate to the GuardDuty console in the region you want to run this scenario in and then click **Get Started**.
![Get Started][./images/screenshot.png]



## License Summary

This sample code is made available under a modified MIT license. See the LICENSE file.
