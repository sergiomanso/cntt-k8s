# Kubernetes Low Level design

## Introduction

Kubernetes is a container orchestration solution originally designed and open sourced by Google. It allows running containers of different kinds (Docker, rkt, containerd) at scale, with interesting properties such as self healing, service discovery and autoscaling. 
The Charmed Kubernetes (CK) offers a solution as close as possible to the upstream version of Kubernetes.
The goal of this document is to explain, the deployment of Kubernetes for CNTT requirements compliant environment. Kubernetes can be deployed on-top of a compliant substrate using Juju. The compliant substrate list includes
- Openstack
- GCP
- AWS

This document contains design details pertaining to:
1. **Design Overview**. The Design Overview provides a high level presentation that describes the Kubernetes Strategy, Architecture, and overall design characteristics.
2. **Charm Bundle**. The Charm Bundle is a YAML file that describes the complete model of the deployed cloud as code. This file can be used to build and rebuild your cloud at any time. 

## Technologies

### Ubuntu Server
The workers will be deployed as virtual machines running Ubuntu operating system. Ubuntu Server is the operating system developed by Canonical for servers and cloud and is the base platform for the whole deployment. Ubuntu is a Linux based operating system with commercial support and follows release cycle available at https://www.ubuntu.com/about/release-cycle.

### Juju
Juju is a service modeling software implemented as a distributed system. It uses a model description as an input and delivers an environment according to a set of requirements defined in the model. It is also used to manage the lifecycle of services in a given model.

Juju consists of a number of components:
- Controller node (physical or virtual) which hosts API and database components of Juju;
  - Controllers include a machine provider-specific provisioning logic (MAAS acts as a machine provider in this case);
- Juju client which is used to bootstrap and manage Juju itself and models provisioned via Juju;
- Machine agents are used to perform post-deployment machine-related tasks that are relevant for Juju operation and report to Juju controller nodes;
- Unit agents execute application lifecycle events. The concrete application-specific logic is encoded in Charms.

A detailed Juju documentation can be found at https://jaas.ai/. 

### Charms
Charms encode the operational knowledge about a particular application in a reusable way. The operational knowledge in question is about deployment, scaling, upgrades, post-deployment reconfiguration, setting up software in a highly available configuration, integrations with other applications etc.

An application provider would typically have the best operational knowledge about a given application and Charms provide a way to express this knowledge in a more sophisticated way than what deployment-focused automation and regular configuration tooling can do.

Charms rely on Juju to provide them with a platform for distributed and event-driven code execution, data exchange and a data model for common operations. However, the specifics of how to use that platform for a particular application are outside of Juju and are implemented in concrete charms.

The generic approach to operations taken in Juju and Charms makes Charms an exceptional tool not only in deploying and operating simple applications like load balancers or web servers but also complex applications such as OpenStack or Kubernetes.

Most of the software deployment in this engagement will be done using Juju and Charms. All charms that will be used in this project are open source and available at https://jujucharms.com.

You can find the  charmed distribution of Kubernetes bundle at https://github.com/charmed-kubernetes/bundle. 

### Charmed Kubernetes

The release cycle of the Charmed Kubernetes (CK) is tightly synchronized to the release of upstream Kubernetes®. The current version and two prior releases are supported, giving an effective support period of nine months, subject to changes in the upstream release cycle. Up-to-date information about Ubuntu and CK  support periods is available at https://www.ubuntu.com/about/release-cycle. 

## Substrate Configuration

### Infrastructure
XXX: TBD. Description of required flavors and Openstack config.

### Services by machine class

## Juju

Juju is deployed in high-available mode, with 3 controller units acting as an active-active cluster.

## Kubernetes

### Architecture

### Networking

Kubernetes will use the Calico CNI plugin to implement the cluster networking. The choice of Calico is primarily to enable the NetworkPolicy feature of Kubernetes. NetworkPolicy objects are similar in purpose to Security Groups in virtual environments like OpenStack or AWS.

### ETCD setup

### Encryption

### Kubernetes master

### Kubernetes worker

### Ingress

## Logging and Monitoring

The solution Logging, Alerting and Monitoring (LMA) Stack offers cluster metrics collection and cluster logs collection. It will be deployed using several software components installed into different, dedicated cloud instances.

## Identity and Authorization

## Seccurity

## Reliability

## Architecture Component Details

