> [!abstract] What is it? **Auto Scaling Groups (ASG)** automatically add or remove EC2 instances to maintain application availability and performance. ASGs are used when workloads change over time and you want capacity to adjust without manual intervention.

## Goal of ASG

The goal is to keep the **right number of instances running** at all times. ASG itself is **free**. You only pay for the underlying resources such as EC2, EBS, and networking.

## What you configure

An ASG is defined by:

- **Minimum capacity**
- **Desired capacity**
- **Maximum capacity**
- **Launch Template** (or older Launch Configuration)

The launch template defines how instances are created and includes the AMI, instance type, EBS volumes, security groups, and user data.

## Behavior

ASG continuously monitors instance health. If an instance becomes unhealthy, ASG **terminates and replaces it automatically**. It can also scale in or out based on demand.

## Scaling with CloudWatch

ASG integrates with **CloudWatch alarms**. Alarms monitor metrics and trigger scaling actions.

Example:

- Average CPU utilization is too high
- CloudWatch alarm fires
- ASG scales out by launching instances
- When load drops, ASG scales in

## Scaling Policies

### Dynamic Scaling

Automatically adjusts capacity based on metrics.

- **Target Tracking**  
    Maintain a target value such as average CPU at 50 percent.
    
- **Step Scaling**  
    Scale by different amounts based on how far a metric crosses a threshold.
    

### Scheduled Scaling

Scale based on **known traffic patterns**, such as business hours.

### Predictive Scaling

Forecasts future load and **scales ahead of time** based on historical data.

## Good Metrics to Scale On

- Average CPU utilization
- Request count per target
- Network in or out for network-bound apps
- Custom CloudWatch metrics

## Cooldown Period

After a scaling activity, ASG enters a **cooldown period**. During this time, no additional scaling actions occur to prevent rapid fluctuations.

> [!tip] Best Practice  
> Use a **pre-baked AMI** so instances start serving traffic faster, reducing cooldown impact.

<br><br>

<span style="float:left">← [[Elastic Load Balancer — SAA]]</span><span style="float:right">[[Amazon RDS]] →</span>