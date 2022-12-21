<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/reference-architecture/blob/master/docs/cleanup.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# Cleanup

To clean and delete all the BoltOps reference architecture components:

## Delete ECS Demo Apps

Delete the frontend app.

    cd demo-frontend
    UFO_ENV=development ufo destroy --sure --no-wait
    UFO_ENV=production  ufo destroy --sure --no-wait

Delete the backend app.

    cd demo-backend
    UFO_ENV=development ufo destroy --sure --no-wait
    UFO_ENV=production  ufo destroy --sure --no-wait

## Delete ECS Cluster EC2 servers

    cd reference-architecture
    LONO_ENV=development lono cfn delete ecs-spot --sure --no-wait
    LONO_ENV=development lono cfn delete ecs-asg  --sure --no-wait
    LONO_ENV=production  lono cfn delete ecs-spot --sure --no-wait
    LONO_ENV=production  lono cfn delete ecs-asg  --sure --no-wait

## Delete VPCs

    cd reference-architecture
    LONO_ENV=development lono cfn delete vpc --sure --no-wait
    LONO_ENV=management  lono cfn delete vpc --sure --no-wait
    LONO_ENV=production  lono cfn delete vpc --sure --no-wait
