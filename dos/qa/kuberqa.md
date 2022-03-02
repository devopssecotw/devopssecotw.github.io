# dos
## Kubernetes
### QA
#### p1
#### p1
- What's Kubernetes?
  Kubernetes is a distributed open-source technology that helps us in scheduling and executing application containers within and across clusters. A Kubernetes cluster consists of two types of resources:

The Master => Coordinates all activities in the cluster, for example, => scheduling applications, maintaining applications' state, scaling applications, and rolling out new updates

Nodes => A node is an instance of an OS that serves as a worker machine in a Kubernetes cluster.

Also, Node will have two components

Kubelet => Agent for managing and communicating with the master
Tool (Docker/containers) => Tools for running container operations

Kubernetes Cluster
It is designed based on ground-up as a loosely coupled collection of containers centered around deploying, maintaining, and scaling workloads. Works as an engine for resolving state by converging actual and the desired state of the system (self-healing). Hidden from the underlying hardware of the nodes and provides a uniform interface for workloads to be both deployed and consume the shared pool of resources(hardware) in order to simplify deployment.

Pods are the smallest unit of objects that can be deployed on Kubernetes, Kubernetes packages one or more containers into a higher-level structure called a pod. Pod runs one level higher to the container.

A POD always runs on a Node but they share a few resources which can be Shared Volumes, Cluster Unique IP, Info about how to run each container.  All containers in the pod are going to be scheduled on an equivalent node.

Services are the unified way of accessing the workloads on the pods, Control plane which is the core of Kubernetes is an API server that lets you query, manipulate the state of an object in Kubernetes.


POD
The following image describes the work-flow of the Kubernetes from a high level, wherein the application description is a YAML file also known as configuration or spec file with the help of which we can deploy applications bundled in the form of pods in cluster or node


Kubernetes Flow








### references
#### links
- <https://www.interviewbit.com/kubernetes-interview-questions/>