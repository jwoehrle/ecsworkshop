+++
title = "Clean up Compute Resources."
chapter = false
weight = 10
+++

Let's clean up our compute resources first:


{{%expand "Expand here to cleanup ecs cli portion of the workshop" %}}

## Delete our compute resources, starting with the services, then ALB, then ECS Cluster, VPC, etc...
```
cd ~/environment/ecsdemo-frontend

ecs-cli compose --project-name ecsdemo-crystal service rm --cluster-config container-demo
ecs-cli compose --project-name ecsdemo-nodejs service rm --cluster-config container-demo
ecs-cli compose --project-name ecsdemo-frontend service rm --delete-namespace --cluster-config container-demo

aws cloudformation delete-stack --stack-name container-demo-alb
aws cloudformation wait stack-delete-complete --stack-name container-demo-alb
aws cloudformation delete-stack --stack-name container-demo
```    
{{% /expand %}}

{{%expand "Expand here to cleanup the cdk portion of the workshop" %}}
## Delete each service stack, and then delete the base platform stack
```bash
cd ~/environment/ecsdemo-frontend/cdk
cdk destroy -f
cd ~/environment/ecsdemo-nodejs/cdk
cdk destroy -f
cd ~/environment/ecsdemo-crystal/cdk
cdk destroy -f
cd ~/environment/container-demo/cdk
cdk destroy -f
```
{{% /expand %}}