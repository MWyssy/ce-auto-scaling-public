# CLI instructions for create an auto-scaling group

## Create a Launch Template

```
aws ec2 create-launch-template \
--launch-template-name <name> \
--version-description <version> \
--launch-template-data '{"ImageId":"ami-09744628bed84e434","InstanceType":"t2.micro","KeyName":"<key-pair>","SecurityGroupIds":["<security-group>"],"UserData":"<encoded-user-data"}'

```

- To create the user data, you need to first write a bash script file, then you need to encode it using the 'base64 -w 0 user-data.sh' command. You can feed the result into a file called 'encoded-user-data.txt' with the '>' symbol, then copy and paste the contents into the launch-template-data JSON.

## Create an Auto-Scaling group

```
aws autoscaling create-auto-scaling-group \
--auto-scaling-group-name <name> \
--launch-template LaunchTemplateId=<launch-template-id> \
--target-group-arns <target-group-arn> \
--min-size <number> \
--max-size <number> \
--desired-capacity <number> \
--vpc-zone-identifier "<subnet1>,<subnet2>,<subnet3>"
```
