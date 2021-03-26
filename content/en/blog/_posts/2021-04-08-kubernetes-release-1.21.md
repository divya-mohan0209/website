---
layout: blog
title: 'Kubernetes 1.21: XXXX'
date: 2021-04-08
slug: kubernetes-1-21-release-announcement
---

**Authors:** [Kubernetes 1.21 Release Team](https://github.com/kubernetes/sig-release/blob/master/releases/release-1.21/release_team.md)

We’re pleased to announce the release of Kubernetes 1.21, our first release of 2021!
This release consists of __ enhancements: __ enhancements have graduated to stable, __ enhancements are moving to beta, and __ enhancements are entering alpha.

## Major Themes

### CronJobs Graduate to Stable!
CronJobs (previously ScheduledJobs) has been a beta feature since Kubernetes 1.8! With 1.21 we get to finally see this widely used API graduate to stable.

CronJobs are meant for performing all time-related actions, namely backups, report generation and the like. Each of these tasks should be allowed to run repeatedly (once a day/month, etc.) or once at a given point in time.
https://github.com/kubernetes/enhancements/issues/19

### IPv4/IPv6 dual-stack support
IP addresses are a consumable resource operators and cluster administrators need to make sure are not exhausted. Having dual-stack support enables native IPv6 routing to pods and services, and it also improves a possible scaling limitation for workloads.

Dual-stack support in Kubernetes means pods, services, and nodes can get IPv4 addresses and IPv6 addresses. In Kubernetes 1.21 dual-stack support is graduating from alpha to beta and is now enabled by default.

### Immutable Secrets and ConfigMaps
Immutable Secrets and ConfigMaps adds a new field to those resource types which will reject changes to those objects if set. Secrets and ConfigMaps by default are mutable which is beneficial for pods that are able to consume changes. Mutating Secrets and ConfigMaps can also cause problems if a bad configuration is pushed for pods that use them.

By marking Secrets and ConfigMaps as immutable you can be sure your application configuration won't change. If you want to make changes you'll need to create a new, uniquly named Secret or ConfigMap and deploy a new pod to consume that resource. Immutable resources also have scaling benefits because controllers do not need to poll the API server to watch for changes.
This feature is now graduating to stable in Kubernetes 1.21.

### Graceful Node Shutdown
Graceful Node shutdown is graduating to beta with this release (and will now be available to a much larger group of users!). This is a hugely beneficial feature that allows Kubelet to be aware of Node shutdown, and gracefully terminate Pods that are scheduled to that Node.

Currently, when a node shuts down, Pods do not follow the expected termination lifecycle and are not shutdown gracefully. This can introduce problems with a lot of different workloads. Going forward, Kubelet will be able to propagate the shutdown signal to Pods ensuring they can terminate as gracefully as possible.

### PV Health Monitor
Physical Volumes (PV) are commonly used in applications to get local, file-based storage. They can be used in many different ways and help users migrate applications without needing to re-write storage backends.

Kubernetes 1.21 has a new alpha feature which allows PVs to be monitored for health of the volume and marked accordingly if the volume becomes unhealthy. Workloads will be able to react to the health state to protect data from being written or read from a volume that is unhealthy.

### Reducing Kubernetes Build Maintenance
Previously Kubernetes has maintained multiple build systems. This has often been a source of friction and complexity for new and current contributors.

Over the last release cycle, a lot of work has been put in to simplify the build process, and standardize on the native Golang build tools. This should empower broader commmunity maintenance, and lower the barier to entry for new contributors.

## Major Changes

### PodSecurityPolicy Deprecation
As of Kubernetes 1.21 PodSecurityPolicies in their current form will be deprecated. Even though the feature has been deprecated, it will continue to be available and function as before until Kubernetes 1.25. Going forward, there is a proposal in place for a simplified feature that will fill the basic use cases of PodSecurityPolicies.

SIG security has prepared a dedicated blog post with more details about the PodSecurityPolicy feature deprecation. You can read that [here.]()

## Other Updates

### Graduated to Stable

* [EndpointSlice](https://github.com/kubernetes/enhancements/issues/752)
* [Add sysctl support](https://github.com/kubernetes/enhancements/issues/34)
* [PodDisruptionBudgets](https://github.com/kubernetes/enhancements/issues/85)

### Notable Feature Updates

* [External client-go credential providers](https://github.com/kubernetes/enhancements/issues/541)
* [Structured logging](https://github.com/kubernetes/enhancements/issues/1602)
* [Jobs and Pods TTL after finish](https://github.com/kubernetes/enhancements/issues/592)

# Release notes

You can check out the full details of the 1.21 release in the [release notes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.21.md).

# Availability of release

Kubernetes 1.21 is available for [download on GitHub](https://github.com/kubernetes/kubernetes/releases/tag/v1.21.0). There are some great resources out there for getting started with Kubernetes. You can check out some [interactive tutorials](https://kubernetes.io/docs/tutorials/) on the main Kubernetes site, or run a local cluster on your machine using Docker containers with [kind](https://kind.sigs.k8s.io). If you’d like to try building a cluster from scratch, check out the [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way) tutorial by Kelsey Hightower.

# Release Team

This release was made possible by a very dedicated group of individuals, who came together as a team in the midst of a lot of things happening out in the world. A huge thank you to the release lead Nabarun Pal, and to everyone else on the release team for supporting each other, and working so hard to deliver the 1.21 release for the community.

# Release Logo

![Kubernetes 1.21 Release Logo](XXXX)



# User Highlights

- CNCF welcomes 47 new organizations across the globe as members to advance Cloud Native technology further at the start of 2021! These [new members](https://www.cncf.io/announcements/2021/02/24/cloud-native-computing-foundation-welcomes-47-new-members-at-the-start-of-2021/) will join CNCF at the upcoming 2021 KubeCon + CloudNativeCon events, including [KubeCon + CloudNativeCom EU – Virtual](https://events.linuxfoundation.org/kubecon-cloudnativecon-europe/) from May 4 – 7, 2021, and [KubeCon + CloudNativeCon NA in Los Angeles](https://events.linuxfoundation.org/kubecon-cloudnativecon-north-america/) from October 12 – 15, 2021.

# Project Velocity

The [CNCF K8s DevStats project](https://k8s.devstats.cncf.io/) aggregates a number of interesting data points related to the velocity of Kubernetes and various sub-projects. This includes everything from individual contributions to the number of companies that are contributing, and is a neat illustration of the depth and breadth of effort that goes into evolving this ecosystem.

In the v1.21 release cycle, which ran for 12 weeks (January 11 to April 8), we saw contributions from [999 companies](https://k8s.devstats.cncf.io/d/9/companies-table?orgId=1&var-period_name=v1.20.0%20-%20now&var-metric=contributions) and [1279 individuals](https://k8s.devstats.cncf.io/d/66/developer-activity-counts-by-companies?orgId=1&var-period_name=v1.20.0%20-%20now&var-metric=contributions&var-repogroup_name=Kubernetes&var-country_name=All&var-companies=All).


# Ecosystem Updates

Master -> Main default branch migration [(PR#21451)](https://github.com/kubernetes/test-infra/pull/21451) is here! This migration divides tests as main and release branches, removes v1alpha2 tests and adds apidiff test, and fixes naming from master to main.


# Event Updates

- KubeCon + CloudNativeCon Europe 2021 will take place May 4 - 7, 2021! Registration opened on January 11. You can find more information about the conference [here](https://events.linuxfoundation.org/kubecon-cloudnativecon-europe/).
- Kubernetes Community Days are being relaunched! Q1 will start with Africa and Bengaluru. You can find more information [here](https://kubernetescommunitydays.org/).

# Upcoming release webinar

Stay tuned for the upcoming release webinar happening this May

# Get Involved

If you’re interested in contributing to the Kubernetes community, Special Interest Groups (SIGs) are a great starting point. Many of them may align with your interests! If there are things you’d like to share with the community, you can join the weekly community meeting, or use any of the following channels:

* Find out more about contributing to Kubernetes at the new [Kubernetes Contributor website](https://www.kubernetes.dev/)
* Follow us on Twitter [@Kubernetesio](https://twitter.com/kubernetesio) for latest updates
* Join the community discussion on [Discuss](https://discuss.kubernetes.io/)
* Join the community on [Slack](http://slack.k8s.io/)
* Share your Kubernetes [story](https://docs.google.com/a/linuxfoundation.org/forms/d/e/1FAIpQLScuI7Ye3VQHQTwBASrgkjQDSS5TP0g3AXfFhwSM9YpHgxRKFA/viewform)
* Read more about what’s happening with Kubernetes on the [blog](https://kubernetes.io/blog/)
* Learn more about the [Kubernetes Release Team](https://github.com/kubernetes/sig-release/tree/master/release-team)
