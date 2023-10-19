# Google Kubernetes Engine vs Azure Kubernetes Engine

Created from information via [Stackrox EKS vs GKE vs AKS](https://www.stackrox.com/post/2021/01/eks-vs-gke-vs-aks-jan2021/)

## Context of assessment

I will be basing my assessment purely out of an easy of use lens. As I have not used Kubernetes before, I would like to go with the abstraction that is easiest for me to use.

I kept my evaluation criteria simple for the sake of simplicity and limited it to Price, Supported Containers, Version maturity, Logging, and release date.

#### Microsoft Azure Kubernetes Engine (AKS)

| Price                    | Pay as you go with optional SLA add-on                       |
| ------------------------ | ------------------------------------------------------------ |
| **Supported Containers** | **Docker, containerd**                                       |
| **Version Maturity**     | **Supports up to 1.20**                                      |
| **Logging**              | **Logs are transmitted to [Azure Monitor](https://azure.microsoft.com/en-us/services/monitor/)** |
| **Release Date**         | **June 2018**                                                |

##### Google Kubernetes Engine (GKS)

| Price                    | $0.10/hour with optional SLA add-on                          |
| ------------------------ | ------------------------------------------------------------ |
| **Supported Containers** | **Docker, containered, gVisor**                              |
| **Version Maturity**     | **1.17**                                                     |
| **Logging**              | **Logs are transmitted to [Google Cloud's Operarations suite](https://cloud.google.com/products/operations)** |
| **Release Date**         | **August 2015**                                              |

## Assessment

#### Price

It is difficult to assess price without actually looking at a concrete case for these abstractions. That said, I would certainly opt for the SLA add-on. Otherwise, why would I even consider offloading the responsibility to the provider?

#### Supported Containers

I chose this one because I was interested to see what each abstraction supported. I have only worked in Docker and have only touched Containered in a personal project. it is more suited for volume-less jobs. I have never used gVisor (or even heard of it.)

> Unlike most kernels, gVisor does not assume or require a fixed set of physical resources; instead, it leverages existing host kernel functionality and runs as a normal process. In other words, gVisor implements Linux by way of Linux. -Gvisor’s github [README](https://github.com/google/gvisor)

How poetic.

#### Version Maturity

It seems as though AKS is faster at supporting newer versions than GKE. This might come into play for zero day fixes. Since I would be just learning the ropes, I don’t think that I would necessarily need the latest and greatest version.

#### Logging

Both abstractions transmit their logs to their respective platform’s logging interfaces.

#### Release date

GKS was released a month after the official launch of Kubernetes.

Some light research lead me to find out an interesting fact: It turns out that Kubernetes was originally released by Google. Later on it was spun off into the responsibility of the “Cloud Native Computing Foundation”, a project founded by Google, RedHat, Twitter, Intel, IBM, Docker, and VMware.

### Conclusion

Based on predicted ease of use, I would go with Google Kubernetes Engine. It has been around the longest and it’s DNA is interwined with the origin of Kubernetes. While Azure has significantly more users than Google Cloud Platform, I believe that there is a much tighter community around GKE than AKS based on the origins of Kubernetes.

