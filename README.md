# Grafana ECS stack with Cloudformation

## To deploy Network Stack
```
aws cloudformation deploy \
  --stack-name network \
  --template-file vpc.yml 
```

## To deploy SG Stack
```
aws cloudformation deploy \
  --stack-name sg \
  --template-file security-groups.yml \
  --parameter-overrides NetworkStackName=network
```

## To deploy IAM Stack
```
aws cloudformation deploy \
  --stack-name iam \
  --template-file iam.yml \
  --capabilities CAPABILITY_NAMED_IAM
```

## To deploy Grafana ECS Stack
```
aws cloudformation deploy \
  --stack-name ecs-grafana \
  --template-file grafana-ecs-full-stack.yml \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameter-overrides \
    NetworkStackName=network  \
    SecurityGroupStackName=sg \
    IamStackName=iam \
    InstanceType=t2.micro \
    KeyName=my-key \
    Route53HostedZone=yourdomain.com. \
    CertificateArn=arn:aws:acm:us-east-1:xxxxx
```