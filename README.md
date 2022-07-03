# aws-dev

Install AWS CLI, Docker, LocalStack, and Terraform: See [MacOS Setup](MacOS_Setup.md).

# AWS CLI Scripts

    localstack start -d

    ./create-ec2-instances

    aws ec2 describe-instances \
      --endpoint-url http://localhost:4566 --profile localstack
