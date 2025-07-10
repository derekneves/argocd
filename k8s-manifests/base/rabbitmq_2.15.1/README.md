# RabbitMQ Installation Guide

As of our current configuration, user and vhost are not created if you apply `/etc/rabbitmq/conf/definitions.json` in additionalConfig. To prevent this, RabbitMQ is installed in two phases.

1. Disable [additionalConfig](https://github.com/flybits/phoenix-kubernetes/commit/c40170ec2e620890435c301bf804621428b7287e)
2. Once the cluster is healthy, enable `additionalConfig` to apply definitions.json (config to apply HA, ...)

#### References:

- RabbitMQ GitHub Issue: https://github.com/docker-library/rabbitmq/issues/365