# Benchmarking tools for deploying Kubernetes clusters

# Introduction
**Our mission to make life easier and create a tool for converting images into ascii-art using Machine Learning**
**There are several tool that can help us in deployments and automation:**
- `minikube`: It's a local Kubernetes system, that allows to create cluster on one machine. 
- `kind (Kubernetes IN Docker)`: It's a tool that allows to create local Kubernetes clusters in Docker containers. 
- `k3d`: It's a tool for creating local Kubernetes clusters in Docker containers using Rancher Kubernetes Engine (RKE)
**Let's analyse their characteristics, advantages and disadvantages to chose proper tool for our case.**

## Characteristics

### Minikube
-  Supports the latest Kubernetes release (+6 previous minor versions)
-  Cross-platform (Linux, macOS, Windows)
-  Deploy as a VM, a container, or on bare-metal
-  Multiple container runtimes (CRI-O, containerd, docker)
-  Direct API endpoint for blazing fast image load and build
-  Advanced features such as LoadBalancer, filesystem mounts, FeatureGates, and network policy
-  Addons for easily installed Kubernetes applications
-  Supports common CI environments

### Kind
-  Go packages implementing cluster creation, image build, etc.
-  A command line interface (kind) built on these packages.
-  Docker image(s) written to run systemd, Kubernetes, etc.
-  kubetest integration also built on these packages (WIP)

### K3d
-  Lightweight Architecture: k3d is minimalistic and uses fewer resources, making it ideal for local development where system resources might be limited.
-  Speed: It allows for rapid deployment and testing of Kubernetes settings, significantly speeding up the development cycle.
-  Ease of Use: With k3d, you can set up a Kubernetes cluster in just a few commands, simplifying what traditionally is a complex process.
-  Docker Integration: k3d runs Kubernetes in Docker containers, seamlessly fitting into Docker-based workflows and toolchains.

## Advantages and disadvantages
### Minikube
#### Advantages
- Easy To Use: Entry barrier seems quite low
- Deployment Speed
- Lower resource consumption
- Ability to run with latest Kubernetes version
- Comprehensive documentation
- All K8s features goes with minikube
#### Disadvantages
- Limited scaling capabilities
- No support for multiple logical clusters
- Poor automation options
### Kind
#### Advantages
- Easy To Use
- Deployment Speed
- Configuration files gives advantages using in a team
- Podman and rootless mode
#### Disadvantages
- 
### K3d
#### Advantages
- Configuration files gives advantages using in a team
- Comprehensive documentation
- Allows to manage multiple separate clusters for development on one host
- Configuration files gives advantages using in a team
- kubectl context automatically set to the newly created cluster
#### Disadvantages
- Only Docker containers
- Does not provide so many features on the command line as minikube
- CLI is not in the box

### Comparison table
| Features            | Minikube                                                | Kind                                                         | K3d                                                |
|---------------------|---------------------------------------------------------|--------------------------------------------------------------|----------------------------------------------------|
| Licence             | Apache License 2.0                                      | Open source, CNCF certified conformant Kubernetes installer  | K-3D is Free Software. GNU General Public License. |
| Multi/Single node   | Single node only                                        | Multi-node (including HA) clusters                           | Multiple worker nodes                              | 
| Cross-platform      | macOS, Linux, and Windows                               | macOS, Linux, and Windows                                    | macOS, Linux, and Windows                          |
| Popularity          | 25.8k stars on GitHub                                   | 11.1k stars on GitHub                                        | 4.1k stars on GitHub                               |
| Types of containers | Multiple container runtimes (CRI-O, containerd, docker) | Docker                                                       | Docker                                             |


## Demo
![Image](demo.gif)

## Conclusions
It is very difficult to pick a winner in this comparison. All three established solutions, minikube, k3d, and kind are very similar to each other. There are some pros and cons for any solution but nothing that really stands out. That’s good because it’s not really possible to choose the wrong tool, either. I like the overall usability of all of these tools, given they address a professional working environment. All of them are fast, easy to install, and quite easy to use.
I have a gut feeling that minikube is slightly ahead of all options and the closest to the official Kubernetes development roadmap. Especially, for a single (potentially inexperienced) developer the entry barrier seems quite low. Yet, it’s the option with the highest resource demands. I would recommend minikube to Kubernetes starters.
At Blueshoe, we have been very happy with k3d in the past. Especially if you run many different Kubernetes clusters, you will be happy about the lower resource consumption compared to minikube. If you are working in a team, the configuration files coming with k3d or kind will be a huge benefit for all.
For some of our automated test cases, we switched over to minikube, because of the --kubernetes-version argument. It’s dead simple to set the requested Kubernetes version and voila, it’s running. With k3d you have to take a look at the corresponding k3s Docker image to use.
In the long run, we actually don’t see local Kubernetes development as a sustainable option. Remote development environments are the future! Getdeck Beiboot will run all Kubernetes-based resources, and with tools like Gefyra, we enable developers to work in a real Kubernetes-based development environment.
