# AWS_boto3
## AWS boto3 : Get all running EC2 instance details

```
import json
import boto3

def lambda_handler(event, context):
    # TODO implement
    ec2 = boto3.resource('ec2')
    region = 'us-east-1'
    condition = [{
        'Name': 'instance-state-name',
        'Values': ['running']
    }]
    all_instances = ec2.instances.filter(Filters=condition)
    instance_ids = []
    for instance in all_instances:
        instance_ids.append(instance.id)
        
    return {
        'statusCode': 200,
        'body': json.dumps('Fetch all running EC2 instance ids!'),
        'instance_ids': instance_ids
    }
```

## AWS boto3 : Stop EC2 instances using EC2 instance ids

```
import json
import boto3

def lambda_handler(event, context):
    # TODO implement
    ec2 = boto3.resource('ec2')
    region = 'us-east-1'
    condition = [{
        'Name': 'instance-state-name',
        'Values': ['running']
    }]
    all_instances = ec2.instances.filter(Filters=condition)
    all_instance_ids = []
    for instance in all_instances:
        all_instance_ids.append(instance.id)
    ec2_stop = boto3.client('ec2')
    ec2_stop.stop_instances(InstanceIds=all_instance_ids)
    return {
        'statusCode': 200,
        'body': json.dumps('EC2 instances stopped successfully!'),
        'instance_ids': instance_ids
    }
    ```
