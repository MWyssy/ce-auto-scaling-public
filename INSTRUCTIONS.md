# CLI instructions for create an auto-scaling group

## Create a Launch Template

```
aws ec2 create-launch-template \
--launch-template-name api-server-launch-template \
--version-description version-1 \
--launch-template-data '{"ImageId":"ami-09744628bed84e434","InstanceType":"t2.micro","KeyName":"learner-api-keypair","SecurityGroupIds":["sg-09165ab621bff9155"],"UserData":"IyEgL2Jpbi9iYXNoCnN1ZG8gYXB0IHVwZGF0ZQpzdWRvIGFwdCBpbnN0YWxsIC15IG5vZGVqcwpzdWRvIGFwdCBpbnN0YWxsIC15IG5wbQpzdWRvIG5wbSBpbnN0YWxsIHBtMiAtZwpnaXQgY2xvbmUgaHR0cHM6Ly9NV3lzc3k6Z2hwX2E0SXFzWFlrS2lCNm5FSzA0dldWbXRLTUtWVGY1bjJHMWdpeUBnaXRodWIuY29tL01XeXNzeS9jZS1sb2FkLWJhbGFuY2luZy1ub2RlLWFwaS5naXQKY2QgY2UtbG9hZC1iYWxhbmNpbmctbm9kZS1hcGkvYXBwCm5wbSBpbnN0YWxsCnBtMiBzdGFydCBzcmMvaW5kZXguanM="}'

```

- To create the user data, you need to first write a bash script file, then you need to encode it using the 'base64 -w 0 user-data.sh' command. You can feed the result into a file called 'encoded-user-data.txt' with the '>' symbol, then copy and paste the contents into the launch-template-data JSON.

## Create an Auto-Scaling group

```
aws autoscaling create-auto-scaling-group \
--auto-scaling-group-name api-server-auto-scaling-group \
--launch-template LaunchTemplateId=lt-08fac9a1db85d5cc3 \
--target-group-arns arn:aws:elasticloadbalancing:eu-west-2:529351201608:targetgroup/api-server-targetgroup/39163dcb11d90771 \
--min-size 2 \
--max-size 5 \
--desired-capacity 3 \
--vpc-zone-identifier "subnet-00298f9683b3fe35e,subnet-0926aeb3c0bc0597e,subnet-05e708d5fdd66fc4f"
```
