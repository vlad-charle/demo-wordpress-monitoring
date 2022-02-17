# demo-wordpress-monitoring

## Project description

This repo contains monitoring, based on DataDog, deployment for my demo project at SoftServe DevOps Crash Course 2021. 

DataDog has implemented BlackBox monitoring via custom metric and monitor, that track number of active nodes and if <2 it triggers PagerDuty to send alert and create incident, and WhiteBox monitoring via Synthetic Tests, that check application availability with GET requests from around the world.

## Project pre-requisites

Jenkins with installed Docker, kubectl, Helm, AWS CLI, AWS Authenticator, Terraform. I used latest Jenkins Docker image and installed all required packages: https://hub.docker.com/r/jenkins/jenkins

DataDog service up & running: https://www.datadoghq.com

PagerDuty service up & running, integrated with DataDog via standard guide: https://www.pagerduty.com/integrations/datadog/

## Project structure

datadog-values.yaml - contains Helm default values to deploy DataDog into the cluster

Jenkinsfile contains the pipeline with the following stages:
1. Add DataDog Helm repo and update it
2. Deploy DataDog with Helm into the cluster
