<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/reference-architecture/blob/master/README.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# BoltOps Reference Architecture

[![Watch the video](https://img.boltops.com/boltopspro/video-preview/reference-architecture.png)](https://youtu.be/uobGIVUG2Xo)

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

Learning to build modern AWS infrastructure can be daunting. The BoltOps reference architecture makes it much easier and more fun. This architecture covers over 80% of use cases, giving you a good bet.

We start with security in mind. The VPC is based on best practices and the [AWS Standardized Architecture for PCI DSS on AWS](https://docs.aws.amazon.com/quickstart/latest/compliance-pci/overview.html). The reference architecture serves as a solid foundation for your company.

![](https://img.boltops.com/boltopspro/blueprints/reference-architecture/reference-architecture.png)

## Blueprints

This repository contains code to build the BoltOps Reference Architecture. It is preconfigured with baseline BoltOps Pro Lono blueprints to build everything. Lono blueprints are essentially CloudFormation templates.

Lono blueprints allow you to configure the templates outside of the code in an organized way. This makes the code reusable.  You simply:

1. Configure
2. Deploy
3. Run

Learn more: [Lono DRY: Reusable Code docs](https://lono.cloud/docs/dry/).

Here's a list of the preconfigured blueprints.

Blueprint  | Description
------------- | -------------
[vpc](https://github.com/boltopspro-docs/vpc)  | The VPC foundation.  The VPC starts with security strong in mind and is based on best practices and the [AWS Standardized Architecture for PCI DSS on AWS](https://docs.aws.amazon.com/quickstart/latest/compliance-pci/overview.html).
[vpc-peer](https://github.com/boltopspro-docs/vpc-peer)  | Peers the VPCs together in different AWS Accounts.  If you're taking the One AWS Account Strategy, use the [vpc-peer-one blueprint](https://github.com/boltopspro-docs/vpc-peer-one) instead.
[ecs-spot](https://github.com/boltopspro-docs/ecs-spot)  | The ECS Spot Architecture used to realized 50%-90% savings with zero commitment. It makes use of Spot Fleets, explained here [What is the Difference Between Spot Fleet vs Spot Instances](https://blog.boltops.com/2018/07/15/what-is-the-difference-between-spot-fleet-vs-spot-instances).
[ecs-asg](https://github.com/boltopspro-docs/ecs-asg)  | The ECS ASG Cluster that provides high availability in the rare event your spot fleets request are not fulfilled, this provides HA.

## Initial Setup

    git clone git@github.com:boltopspro/reference-architecture
    cd reference-architecture
    bundle

If you are not a BoltOps Pro customer, the `bundle` will fail on the `git pull`.  Check out [BoltOps Pro Subscription](https://boltops.com/pro) if you are interested in access.

The next steps provide on guide on how to **configure, deploy, and run** each of the blueprints.

## Setup AWS_PROFILE

* [AWS_PROFILE and configs/settings.yml Setup](https://github.com/boltopspro-docs/reference-architecture/blob/master/docs/settings-setup.md)

## Create VPCs

Refer to the [VPC Blueprint](https://github.com/boltopspro-docs/vpc)

At this point, we can create resources like EC2 Instances, ECS Clusters, ELBs on any of the newly created VPCs.

## Peer the VPCs

Refer to the [VPC Peer Blueprint](https://github.com/boltopspro-docs/vpc-peer)

At this point, we have peered the management VPC with the development and production VPCs.

## Create ECS Spot Clusters

Refer to the [ECS Spot Blueprint](https://github.com/boltopspro-docs/ecs-spot)

At this point, we have created the spot fleets for the ECS clusters.

## Create ECS ASG Clusters

Refer to the [ECS ASG Blueprint](https://github.com/boltopspro-docs/ecs-asg)

At this point, we have created the Highly Available Spot Architecture.

## Deploy Demo Apps

Deploy a backend and frontend app on top of the reference architecture.

* [Demo Backend App](https://github.com/boltopspro-docs/demo-backend)
* [Demo Frontend App](https://github.com/boltopspro-docs/demo-frontend)

At this point, we deploy a backend application with an internal ELB and a frontend application with a public-facing ELB.

## Summary

After completing all the sections above, you have successfully deployed an application to the Highly Available Spot Architecture. Congrats 🎉
