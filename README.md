# Lambda Function for Creating AMIs using EventBridge Schedule

This CloudFormation template deploys a Lambda function that creates Amazon Machine Images (AMIs) based on a schedule defined in Amazon EventBridge. This can be useful for automated backups or snapshotting of EC2 instances.

## Supported parameters:
`createAmisAt`: cron schedule to create AMIs, by default at midnight. More: https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-cron-expressions.html

`createAmisLambdaTimeout`: If you have lots of ec2 instances - it requires to adjust this parameter

`deleteOldAmisAt`: cron schedule to delete old AMIs, by default at 2AM. More: https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-cron-expressions.html

`keepAmis`: How much AMIs you'd like to keep, 3 by default

`rotateAmisLambdaTimeout`: If you have lots of AMIs - it requires to adjust this parameter

## Deployment Steps

### Using AWS CLI

1. **Prerequisites**: Ensure you have AWS CLI installed and configured with the necessary permissions.

2. **Clone the Repository**: Clone this GitHub repository to your local machine.

   ```bash
   git clone https://github.com/RealArtemiy/ami-scheduler.git
   ```

3. **Navigate to Template Directory**: Enter into the directory containing your CloudFormation template.

   ```bash
   cd ami-scheduler
   ```

4. **Deploy Stack**: Use the AWS CLI to deploy the CloudFormation stack. Replace `<stack_name>` with your desired stack name.

   ```bash
   aws cloudformation create-stack --stack-name <stack_name> --template-body file://cloudformation.yml --capabilities CAPABILITY_IAM
   ```

5. **Monitor Deployment**: Monitor the stack creation process either via the AWS Management Console or using the AWS CLI.

   ```bash
   aws cloudformation describe-stacks --stack-name <stack_name> --query "Stacks[0].StackStatus"
   ```

### Using AWS Management Console (UI)

1. **Sign in to AWS Console**: Sign in to your AWS Management Console.

2. **Navigate to CloudFormation**: Go to the CloudFormation service.

3. **Create Stack**: Click on "Create stack" and choose "With new resources (standard)".

4. **Upload Template**: Upload the CloudFormation template file (`cloudfomation.yml`).

5. **Specify Stack Details**: Provide a stack name and any necessary parameters.

6. **Configure Stack Options**: Configure stack options as needed, then proceed to create the stack.

7. **Monitor Deployment**: Monitor the stack creation process in the CloudFormation dashboard.

---

Resources to be created:
- AWS::Lambda::Function
- AWS::IAM::Role	
- AWS::Lambda::Permission	
- AWS::Events::Rule