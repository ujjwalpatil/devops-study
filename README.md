# devops-study
# DevOps, Cloud Infrastructure & Platform Engineering Interview Guide

This guide covers the core technical topics for DevOps, Cloud Infrastructure, SRE, and Platform Engineering interview rounds. It is organized **by topic**: each topic has one home (for example, everything about Spinnaker is in Part 7, and everything about Kubernetes networking is in Part 4), with its subtopics beneath it. The contents list below links to every part, section and subsection.

## Contents

### Start here
* [How to use it: study paths](#how-to-use-it-study-paths)
* [Architect and platform round focus areas](#architect-and-platform-round-focus-areas)
* [Reference architecture: cell-based multi-region SaaS platform](#reference-architecture-cell-based-saas-platform)
* [How to approach the architect rounds](#how-to-approach-the-architect-rounds)

### [Part 1: AWS: networking, load balancing, IAM, compute and troubleshooting](#part-1-aws-networking-load-balancing-iam-compute-and-troubleshooting)
* [1.1 The picture to keep in your head](#11-the-picture-to-keep-in-your-head)
* [1.2 Security groups (SGs)](#12-security-groups-sgs)
* [1.3 Network ACLs (NACLs)](#13-network-acls-nacls)
* [1.4 Security group versus NACL, side by side](#14-security-group-versus-nacl-side-by-side)
* [1.5 Target groups](#15-target-groups)
* [1.6 Application Load Balancer (ALB): Layer 7](#16-application-load-balancer-alb-layer-7)
* [1.7 Network Load Balancer (NLB): Layer 4](#17-network-load-balancer-nlb-layer-4)
* [1.8 ALB or NLB](#18-alb-or-nlb)
* [1.9 nginx on AWS](#19-nginx-on-aws)
* [1.10 The chain, and how timeouts should line up](#110-the-chain-and-how-timeouts-should-line-up)
* [1.11 DNS, edge and connecting networks](#111-dns-edge-and-connecting-networks)
* [1.12 Networking depth: questions a networking-minded architect asks](#112-networking-depth-questions-a-networking-minded-architect-asks)
* [1.13 IAM in plain terms](#113-iam-in-plain-terms)
* [1.14 Compute and storage essentials, explained](#114-compute-and-storage-essentials-explained)
  * [EC2 instances and instance families](#ec2-instances-and-instance-families)
  * [Nitro: why instance size has hard limits](#nitro-why-instance-size-has-hard-limits)
  * [Burstable instances and CPU credits](#burstable-instances-and-cpu-credits)
  * [Auto Scaling Groups (ASGs)](#auto-scaling-groups-asgs)
  * [Spot instances](#spot-instances)
  * [AMIs and Packer (golden images)](#amis-and-packer-golden-images)
  * [IMDSv2 (the instance metadata service)](#imdsv2-the-instance-metadata-service)
  * [EBS (block disks for EC2)](#ebs-block-disks-for-ec2)
  * [S3 (object storage)](#s3-object-storage)
  * [RDS (managed relational databases)](#rds-managed-relational-databases)
* [1.15 Troubleshooting AWS and network traffic](#115-troubleshooting-aws-and-network-traffic)
* [1.16 More AWS troubleshooting scenarios](#116-more-aws-troubleshooting-scenarios)

### [Part 2: Terraform](#part-2-terraform)
* [2.1 Configuration, state, plan and reality are four different things](#21-configuration-state-plan-and-reality-are-four-different-things)
* [2.2 How Terraform talks to AWS (the first-time walkthrough)](#22-how-terraform-talks-to-aws-the-first-time-walkthrough)
* [2.3 The core concepts in five lines](#23-the-core-concepts-in-five-lines)
* [2.4 Modules, environments, workspaces and cells](#24-modules-environments-workspaces-and-cells)
* [2.5 Questions you will likely get](#25-questions-you-will-likely-get)
* [2.6 Terraform question bank, with explained answers](#26-terraform-question-bank-with-explained-answers)
  * [Basics](#basics)
  * [Intermediate](#intermediate)
  * [Advanced](#advanced)
  * [Troubleshooting Terraform](#troubleshooting-terraform)

### [Part 3: Kubernetes fundamentals](#part-3-kubernetes-fundamentals)
* [3.1 What Kubernetes does](#31-what-kubernetes-does)
* [3.2 Requests, limits, probes and graceful shutdown](#32-requests-limits-probes-and-graceful-shutdown)
* [3.3 StatefulSets: what they are, how they work, when to use them](#33-statefulsets-what-they-are-how-they-work-when-to-use-them)
* [3.4 Rapid-fire Kubernetes concepts](#34-rapid-fire-kubernetes-concepts)
* [3.5 Kubernetes performance and security in brief (overview)](#35-kubernetes-performance-and-security-in-brief-overview)

### [Part 4: Kubernetes networking, ingress, service discovery and service mesh](#part-4-kubernetes-networking-ingress-service-discovery-and-service-mesh)
* [4.1 Kubernetes networking, end to end (and the AWS tie-in)](#41-kubernetes-networking-end-to-end-and-the-aws-tie-in)
* [4.2 Ingress, traffic management and DNS at scale](#42-ingress-traffic-management-and-dns-at-scale)
* [4.3 Service discovery, service mesh and Istio](#43-service-discovery-service-mesh-and-istio)
  * [4.3.1 Service discovery: how does service A find service B?](#431-service-discovery-how-does-service-a-find-service-b)
  * [4.3.2 What a service mesh actually does, step by step](#432-what-a-service-mesh-actually-does-step-by-step)
  * [4.3.3 Istio specifics](#433-istio-specifics)
  * [4.3.4 Istio in practice: configuration examples](#434-istio-in-practice-configuration-examples)
  * [4.3.5 Consul (HashiCorp): service registry and service mesh](#435-consul-hashicorp-service-registry-and-service-mesh)

### [Part 5: EKS architecture and platform design](#part-5-eks-architecture-and-platform-design)
* [5.1 EKS architecture in depth](#51-eks-architecture-in-depth)
* [5.2 EKS specifics](#52-eks-specifics)
* [5.3 The design decisions an architect must defend](#53-the-design-decisions-an-architect-must-defend)
  * [5.3.1 Operating a fleet of about 100 clusters (a cell-based platform)](#531-operating-a-fleet-of-about-100-clusters-a-cell-based-platform)
* [5.4 Taking a new containerized service to production on EKS (end to end)](#54-taking-a-new-containerized-service-to-production-on-eks-end-to-end)
  * [5.4.1 What must exist on the platform first](#541-what-must-exist-on-the-platform-first)
  * [5.4.2 Make the container production-ready](#542-make-the-container-production-ready)
  * [5.4.3 Describe the service to Kubernetes](#543-describe-the-service-to-kubernetes)
  * [5.4.4 Access control (who and what may do what)](#544-access-control-who-and-what-may-do-what)
  * [5.4.5 Ingress: traffic coming in](#545-ingress-traffic-coming-in)
  * [5.4.6 Egress: traffic going out](#546-egress-traffic-going-out)
  * [5.4.7 Service-to-service communication](#547-service-to-service-communication)
  * [5.4.8 Security hardening](#548-security-hardening)
  * [5.4.9 Observability](#549-observability)
  * [5.4.10 Scaling and resilience](#5410-scaling-and-resilience)
  * [5.4.11 Delivery and release](#5411-delivery-and-release)
  * [5.4.12 Production readiness review (the gate to go live)](#5412-production-readiness-review-the-gate-to-go-live)
* [5.5 Common Kubernetes problems at large scale, and how to avoid them](#55-common-kubernetes-problems-at-large-scale-and-how-to-avoid-them)
* [5.6 Running data and analytics platforms on EKS (JupyterHub, Airflow, ShinyProxy, Immuta, Airbyte)](#56-running-data-and-analytics-platforms-on-eks-jupyterhub-airflow-shinyproxy-immuta-airbyte)

### [Part 6: Autoscaling, headroom and Karpenter](#part-6-autoscaling-headroom-and-karpenter)
* [6.1 Autoscaling for spiky login traffic (a morning peak or a retry storm)](#61-autoscaling-for-spiky-login-traffic-a-morning-peak-or-a-retry-storm)
  * [Level 1: scaling pods with the HPA (and KEDA)](#level-1-scaling-pods-with-the-hpa-and-keda)
  * [Level 2: scaling nodes, and the headroom problem](#level-2-scaling-nodes-and-the-headroom-problem)
  * [Level 3: protection and dependencies](#level-3-protection-and-dependencies)
* [6.2 Managing pod scaling in day-to-day operations](#62-managing-pod-scaling-in-day-to-day-operations)
* [6.3 Karpenter in depth](#63-karpenter-in-depth)
  * [6.3.1 Configuring and using Karpenter, step by step](#631-configuring-and-using-karpenter-step-by-step)

### [Part 7: Delivery: Helm, Spinnaker and GitOps](#part-7-delivery-helm-spinnaker-and-gitops)
* [7.1 Helm in depth: charts, version files, values and releases](#71-helm-in-depth-charts-version-files-values-and-releases)
* [7.2 Platform-provided Helm charts ("golden charts")](#72-platform-provided-helm-charts-golden-charts)
* [7.3 GitOps with Argo CD](#73-gitops-with-argo-cd)
* [7.4 Spinnaker: everything in one place](#74-spinnaker-everything-in-one-place)
  * [What Spinnaker is, and its vocabulary](#what-spinnaker-is-and-its-vocabulary)
  * [How a Helm deployment runs in Spinnaker](#how-a-helm-deployment-runs-in-spinnaker)
  * [Deploying different Helm versions to many clusters with ONE common pipeline (Pattern B)](#deploying-different-helm-versions-to-many-clusters-with-one-common-pipeline-pattern-b)
  * [Other patterns (short)](#other-patterns-short)
  * [Operating Spinnaker: what to get right in practice](#operating-spinnaker-what-to-get-right-in-practice)
* [7.5 Argo CD versus Spinnaker in detail](#75-argo-cd-versus-spinnaker-in-detail)

### [Part 8: Kubernetes security, secrets and certificates](#part-8-kubernetes-security-secrets-and-certificates)
* [8.1 Kubernetes security architecture (layered)](#81-kubernetes-security-architecture-layered)
* [8.2 Secrets: External Secrets Operator versus Secrets Store CSI driver](#82-secrets-external-secrets-operator-versus-secrets-store-csi-driver)
* [8.3 Certificate management in Kubernetes](#83-certificate-management-in-kubernetes)
* [8.4 A secure software supply chain and deployment platform](#84-a-secure-software-supply-chain-and-deployment-platform)
* [8.5 An air-gapped (federal) EKS environment](#85-an-air-gapped-federal-eks-environment)

### [Part 9: Observability, monitoring and incident response](#part-9-observability-monitoring-and-incident-response)
* [9.1 The tools in plain terms](#91-the-tools-in-plain-terms)
* [9.2 SLOs, burn rate and alert quality](#92-slos-burn-rate-and-alert-quality)
* [9.3 Incident response](#93-incident-response)
* [9.4 Using generative AI for incident triage](#94-using-generative-ai-for-incident-triage)
* [9.5 Observability for Kubernetes on AWS](#95-observability-for-kubernetes-on-aws)
  * [9.5.1 Getting Kubernetes data into Splunk (and other monitoring tools): how it works](#951-getting-kubernetes-data-into-splunk-and-other-monitoring-tools-how-it-works)
* [9.6 Observability for a fleet of EKS clusters](#96-observability-for-a-fleet-of-eks-clusters)

### [Part 10: Kubernetes troubleshooting and performance](#part-10-kubernetes-troubleshooting-and-performance)
* [10.1 Kubernetes troubleshooting by symptom](#101-kubernetes-troubleshooting-by-symptom)
* [10.2 Debugging pod performance issues on EKS](#102-debugging-pod-performance-issues-on-eks)
  * [Step 1: Define the symptom precisely](#step-1-define-the-symptom-precisely)
  * [Step 2: Locate where the time goes](#step-2-locate-where-the-time-goes)
  * [Step 3: Check the pod's resources](#step-3-check-the-pods-resources)
  * [Step 4: Check the node and the neighborhood](#step-4-check-the-node-and-the-neighborhood)
  * [Step 5: Look inside the process](#step-5-look-inside-the-process)
  * [Step 6: Consider scheduling, startup and scaling](#step-6-consider-scheduling-startup-and-scaling)
  * [A quick decision guide](#a-quick-decision-guide)
* [10.3 Kubernetes troubleshooting scenarios](#103-kubernetes-troubleshooting-scenarios)

### [Part 11: Databases and Redis](#part-11-databases-and-redis)
* [11.1 "The database is slow": a method](#111-the-database-is-slow-a-method)
* [11.2 The ideas to explain](#112-the-ideas-to-explain)
* [11.3 Zero-downtime upgrades and schema changes](#113-zero-downtime-upgrades-and-schema-changes)
* [11.4 Monolith, partitioning or sharding](#114-monolith-partitioning-or-sharding)
* [11.5 Redis](#115-redis)

### [Part 12: System design and reliability](#part-12-system-design-and-reliability)
* [12.1 Reliability and design essentials (cells, DR, deployments, resilience)](#121-reliability-and-design-essentials-cells-dr-deployments-resilience)
* [12.2 A multi-tenant EKS platform for 100+ product teams](#122-a-multi-tenant-eks-platform-for-100-product-teams)
* [12.3 A multi-region platform for a login service (99.99 percent or better)](#123-a-multi-region-platform-for-a-login-service-9999-percent-or-better)
* [12.4 Migrating an existing ECS service to EKS](#124-migrating-an-existing-ecs-service-to-eks)
* [12.5 Upgrading 100 clusters with no downtime](#125-upgrading-100-clusters-with-no-downtime)
* [12.6 Surviving the loss of an availability zone](#126-surviving-the-loss-of-an-availability-zone)
* [12.7 Disaster recovery for Kubernetes workloads](#127-disaster-recovery-for-kubernetes-workloads)

### [Part 13: Kubernetes in a networking solution (Nokia EDA)](#part-13-kubernetes-in-a-networking-solution-nokia-eda)
* [13.1 Why Kubernetes suits a network automation platform](#131-why-kubernetes-suits-a-network-automation-platform)
* [13.2 A reference architecture on Kubernetes](#132-a-reference-architecture-on-kubernetes)
* [13.3 Operating it](#133-operating-it)
* [13.4 Failure modes to know](#134-failure-modes-to-know)
* [13.5 A worked example you can adapt for an interview](#135-a-worked-example-you-can-adapt-for-an-interview)
* [13.6 Questions you may get about this example, with answers](#136-questions-you-may-get-about-this-example-with-answers)
* [13.7 If you meant event-driven architecture (the general pattern)](#137-if-you-meant-event-driven-architecture-the-general-pattern)

### [Part 14: Linux, coding and scripting](#part-14-linux-coding-and-scripting)
* [14.1 Linux essentials](#141-linux-essentials)
* [14.2 Coding and scripting tasks for SRE and DevOps interviews](#142-coding-and-scripting-tasks-for-sre-and-devops-interviews)

### [Part 15: Interview preparation: interviewer scenarios, short answers, questions and checklists](#part-15-interview-preparation-interviewer-scenarios-short-answers-questions-and-checklists)
* [15.1 Scenario questions for platform and SRE architect rounds](#151-scenario-questions-for-platform-and-sre-architect-rounds)
* [15.2 Six short answers](#152-six-short-answers)
* [15.3 Questions to ask the interviewer (general)](#153-questions-to-ask-the-interviewer-general)
* [15.4 Final checklist (general)](#154-final-checklist-general)
* [15.5 Questions to ask the architect or platform lead](#155-questions-to-ask-the-architect-or-platform-lead)
* [15.6 Checklist for the architect round](#156-checklist-for-the-architect-round)

### [Part 16: Configuration management with Ansible and immutable infrastructure](#part-16-configuration-management-with-ansible-and-immutable-infrastructure)
* [16.1 Where Ansible fits alongside Terraform and Packer](#161-where-ansible-fits-alongside-terraform-and-packer)
* [16.2 Ansible architecture: inventory, playbooks, roles and idempotency](#162-ansible-architecture-inventory-playbooks-roles-and-idempotency)
* [16.3 Secrets, handlers, templates and safe rollouts](#163-secrets-handlers-templates-and-safe-rollouts)
* [16.4 Ansible in CI/CD and common interview questions](#164-ansible-in-ci-cd-and-interview-questions)

### [Part 17: CI/CD pipelines, containers and cloud-native architecture patterns](#part-17-ci-cd-pipelines-containers-and-cloud-native-architecture-patterns)
* [17.1 CI/CD pipeline design (GitHub Actions, GitLab CI, Jenkins)](#171-ci-cd-pipeline-design-github-actions-gitlab-ci-jenkins)
* [17.2 Docker and container internals deep dive](#172-docker-and-container-internals-deep-dive)
* [17.3 AWS serverless, messaging and managed data patterns](#173-aws-serverless-messaging-and-managed-data-patterns)
* [17.4 High-level system design playbook for DevOps and platform roles](#174-high-level-system-design-playbook-for-devops-and-platform-roles)

---

## How to use it: study paths

Read the explanation, then say the "Say it like this" lines out loud. Speaking turns reading into interview skill.

| If your round is mostly about... | Read these parts | Time |
| :--- | :--- | :--- |
| **A first technical round (AWS, Terraform, Kubernetes basics, troubleshooting)** | Part 1 (AWS), Part 2 (Terraform), Part 3 (Kubernetes fundamentals), Part 9 sections 1 to 4, Part 11 (databases), Part 12 first section, Part 14 (coding) | about 2 hours |
| **Kubernetes, Spinnaker, Helm and pod issues (the SRE architect round)** | Part 5 (EKS architecture), Part 6 (autoscaling and Karpenter), Part 7 (Helm, Spinnaker, GitOps), Part 8 (security, secrets, certificates), Part 10 (troubleshooting), Part 4 (networking and mesh) | about 2.5 hours |
| **System design questions** | Part 12 (design and reliability), then Part 5 section on onboarding a service, Part 9 (observability) | about 1 hour |
| **Leadership and behavioral questions** | Part 15 | 15 minutes |
| **If you work on a Kubernetes-based networking automation platform** | Part 13 | 20 minutes |

## Architect and platform round focus areas

**Core themes in senior DevOps, SRE, and Cloud Platform interviews.** Principal/staff infrastructure architects and platform leads evaluate how you design, operate, and scale production cloud environments with low operational overhead and clear blast-radius isolation:

* **Fleet management at scale:** migrating legacy workloads (EC2 and ECS) to EKS in a cell-based architecture (tens to hundreds of clusters), keeping cluster versions, add-ons, and policies consistent across rings.
* **Infrastructure as Code & Configuration Management:** Terraform for cloud infrastructure and clusters, Ansible and Packer for configuration management and golden images, and GitOps (Argo CD) or continuous delivery pipelines (Spinnaker) for workloads.
* **Platform-as-a-Product:** golden Helm charts provided by the platform team so application teams supply minimal values while getting security, observability, and resilience defaults out of the box.
* **Secrets, autoscaling, and FinOps:** External Secrets Operator versus Secrets Store CSI driver, HPA, KEDA, Karpenter, Cluster Autoscaler, scale-to-zero, and spot instances—along with the failure modes of each.
* **Mixed workloads:** running both latency-sensitive stateless microservices and bursty batch/analytics platforms (JupyterHub, Airflow, ShinyProxy, Immuta, Airbyte) on shared or isolated node pools.
* **Networking depth:** VPC CNI, MTU black holes, SNAT/NAT exhaustion, BGP/Direct Connect, load balancing (ALB/NLB/nginx), service discovery, and service mesh (Istio/Consul).
* **Security and reliability by default:** zero-trust workload identity (IRSA/Pod Identity), mTLS, supply-chain signing, admission policies, SLO burn-rate alerting, and air-gapped/regulated deployments.

**Quick index for high-frequency architect questions:** Helm version files (7.1), continuous delivery pipelines and per-cluster versions (7.4, plus Argo CD comparison in 7.5), Karpenter configuration (6.3.1), pod scaling operations (6.1 and 6.2), certificate management (8.3), Istio (4.3 to 4.3.5), debugging pod performance (10.2), Splunk and observability in Kubernetes (9.5.1), StatefulSets (3.3), operating a 100-cluster fleet (5.3.1), platform Helm charts (7.2), secrets management (8.2), networking depth (1.12), data platforms on EKS (5.6), Ansible (Part 16), CI/CD & system design patterns (Part 17), and scenario questions (Part 15).

**How to engage senior architects.** Show structured engineering judgment: state your assumptions, present the trade-offs, name the failure modes, and specify what metrics or SLOs you would measure.

## Reference architecture: cell-based multi-region SaaS platform

Many large-scale multi-tenant SaaS platforms (identity providers, fintech platforms, enterprise B2B clouds) use a **cell-based architecture** to achieve 99.99%+ availability and isolate blast radius:

* **Scope:** Leading SRE and platform teams across edge networking, Kubernetes platforms, CI/CD, observability, and automation for high-throughput, mission-critical services across multiple availability zones and regions.
* **Cell architecture:** The service runs as many independent copies called **cells**. Each cell holds a complete stack: edge and load balancers, application tiers, caches, and databases. Replicas sit in a second region for disaster recovery, often including a deliberately delayed replica for recovering from bad writes or logical corruption.
* **Data tier:** Often one primary relational database per cell (MySQL or PostgreSQL) scaled vertically and isolated per cell, alongside Redis for caching/rate-limiting and OpenSearch for search/analytics.
* **Delivery & IaC:** Kubernetes (EKS/GKE) with Argo CD (GitOps) or Spinnaker; Terraform for cloud infrastructure; Ansible and Packer for configuration management and immutable machine images.
* **Observability:** Prometheus/Mimir, Loki, Grafana, Splunk, Datadog, OpenTelemetry, CloudWatch, and synthetic edge monitoring (e.g., ThousandEyes).
* **Compliance environments:** Multi-cloud (AWS/GCP) and isolated air-gapped/regulated environments (e.g., FedRAMP/GovCloud).

---

## How to approach the architect rounds

**Core competencies tested in architect rounds.** Multi-region Kubernetes on **EKS and GKE** with **Helm**, **Karpenter**, **Istio** service mesh, **Argo CD and GitOps**, Terraform, and Ansible; migrations from **ECS/EC2 to EKS**; cloud networking fundamentals (DNS, service discovery, ingress, load balancing, TLS, traffic management); reliability guardrails (SLOs, resilience, operational readiness); and regulated/air-gapped clusters (no internet egress, private registries, vendored Helm charts). Expect an architect's conversation: requirements first, then design, trade-offs, failure modes, rollout, security, observability and cost.

**How to answer a design question as an architect (60 seconds of structure).**

1. **Clarify:** users, scale (clusters, services, requests per second, tenants), availability target, compliance, team size, existing constraints.
2. **State assumptions** and success measures (SLOs, adoption, cost).
3. **Draw the simple design first,** then the decisions that matter, each with the alternative you rejected and why.
4. **Failure modes and blast radius:** what breaks, how you detect it, how you limit it.
5. **Rollout and migration:** pilot, canary, rollback.
6. **Security, observability, cost** as built-in parts, not extras.

---

# Part 1: AWS: networking, load balancing, IAM, compute and troubleshooting

## 1.1 The picture to keep in your head

```text
Internet
   |
[Internet gateway]
   |
Public subnets (one per zone):    load balancers (ALB / NLB), NAT gateways, sometimes an nginx edge tier
   |
Private app subnets:              EC2 or Kubernetes nodes and pods, services, nginx
   |
Private data subnets:             RDS, ElastiCache
```

A **VPC** is your private network with an address range you choose (for example 10.0.0.0/16). **Subnets** are slices of it, each in one availability zone. A subnet is **public** when its route table sends internet traffic to an internet gateway, and **private** when it does not. **NAT gateways** (one per zone) let private servers start outbound connections without being reachable from outside. **Route tables** decide where traffic for each destination goes.

## 1.2 Security groups (SGs)

**What it is.** A virtual firewall attached to a network interface (so to an instance, a load balancer, a database, or a Kubernetes pod when pod security groups are used), not to a subnet.

**How it behaves.**

* **Stateful.** If a request is allowed in, the reply is automatically allowed out, and the other way round. You never write a rule for the reply.
* **Allow rules only.** There is no deny. Anything not explicitly allowed is blocked.
* **Defaults.** A new security group allows no inbound traffic and all outbound traffic.
* **A rule** has a protocol, a port range, and a source (inbound) or destination (outbound): an IP range (CIDR), another security group, or a managed prefix list.
* **All rules are evaluated together,** and the most permissive match applies. There is no ordering.
* **Changes apply immediately,** though connections already being tracked may continue until they close.
* **Quotas:** by default about 60 inbound and 60 outbound rules per group (adjustable) and 5 groups per network interface. These matter at scale, especially in Kubernetes.

**Best practice: reference groups, not IP addresses.** A rule that says "allow port 8080 from the load balancer's security group" keeps working when addresses change and instances scale out. A typical layered design:

| Security group | Inbound rule |
| :--- | :--- |
| load balancer | 443 from the internet (0.0.0.0/0) |
| application | 8080 from the load balancer's group only |
| database | 3306 from the application's group only |

A database group that trusts only the application group means a compromised random server cannot even reach the database port.

**Say it like this.** "Security groups are stateful allow-lists on the network interface. I chain them by referencing groups, so each tier only accepts traffic from the tier in front of it, and I do not rely on IP lists."

## 1.3 Network ACLs (NACLs)

**What it is.** A firewall at the subnet boundary. It filters traffic entering and leaving the subnet.

**How it behaves.**

* **Stateless.** It judges every packet by itself, so you must allow the request **and** the reply. Replies go back to the client on a high-numbered temporary (ephemeral) port, so you need an outbound rule for something like ports 1024 to 65535 (and an inbound rule for the same range when your servers make outbound calls and the replies come back in).
* **Allow and deny rules,** each with a number. Rules are checked from the lowest number up, and the **first match wins**. A final catch-all rule denies anything unmatched.
* **Defaults.** The default NACL allows everything. A custom NACL denies everything until you add rules.
* **One NACL per subnet,** but one NACL can serve many subnets.
* **Scope.** It applies to traffic crossing the subnet boundary, not traffic between two instances in the same subnet. It does not filter VPC DNS resolver or instance metadata traffic.

Example for a public subnet that serves web traffic:

| Direction | Rule | Action | Protocol and ports | Source or destination |
| :--- | :--- | :--- | :--- | :--- |
| Inbound | 50 | Deny | all | a known bad range (checked first because 50 is lower) |
| Inbound | 100 | Allow | TCP 443 | 0.0.0.0/0 |
| Inbound | 110 | Allow | TCP 1024-65535 | 0.0.0.0/0 (replies to outbound calls) |
| Outbound | 100 | Allow | TCP 1024-65535 | 0.0.0.0/0 (replies to users) |
| Outbound | 110 | Allow | TCP 443 | 0.0.0.0/0 (calls going out) |

**Why teams use them.** As a coarse backstop, or to block a specific abusive range at subnet level, because security groups cannot deny. Most designs leave NACLs permissive and use security groups for real control.

**The classic outage.** Someone adds a restrictive NACL and forgets the ephemeral-port rule for replies, so connections hang even though the security groups look perfect.

## 1.4 Security group versus NACL, side by side

| | Security group | NACL |
| :--- | :--- | :--- |
| Attached to | A network interface (instance, load balancer, database, pod) | A subnet |
| Stateful or stateless | Stateful | Stateless |
| Rules | Allow only | Allow and deny |
| Rule order | All evaluated together | Lowest number first, first match wins |
| Replies | Automatic | Must be allowed explicitly |
| Typical use | Main per-resource control | Subnet-wide backstop, blocking a range |
| Troubleshooting clue | Times out only to some resources | Whole subnet affected, or replies missing |

A packet must be allowed by **both**: inbound traffic passes the subnet's NACL and then the instance's security group; outbound goes the other way.

## 1.5 Target groups

**What it is.** The list of destinations a load balancer sends traffic to, together with the rules for how to check them. A load balancer listener (for example HTTPS on port 443) forwards to one or more target groups.

**The parts.**

* **Target type:** *instance* (EC2 instances), *ip* (any private address, such as Kubernetes pods or on-premises servers over a private link), *lambda* (a function), or *alb* (an NLB can forward to an ALB).
* **Protocol and port** used to reach the targets.
* **Health check:** protocol, path, port, interval, timeout, how many successes make a target healthy and how many failures make it unhealthy, and which response codes count as success. Typical ALB defaults: 30-second interval, 5-second timeout, 5 successes to become healthy, 2 failures to become unhealthy, success code 200. Tune so unhealthy targets leave quickly but a slow start does not cause flapping.
* **Health states:** initial, healthy, unhealthy, draining (being removed), and unused (the group is not attached to a load balancer, or the target's zone is not enabled).
* **Deregistration delay** (300 seconds by default): when a target is removed, the load balancer lets in-flight requests finish for this long. Applications must shut down gracefully within it, or users see errors on every deploy.
* **Slow start** (ALB): gradually ramps traffic to a new target.
* **Algorithm:** an ALB can use round robin or least outstanding requests; an NLB hashes each connection to a target.
* **Stickiness:** send the same client to the same target (helps stateful apps, but unbalances load).
* **Weights across target groups:** a listener rule can split traffic by percentage between target groups, the basis of blue/green and canary releases.

**Troubleshooting.** `aws elbv2 describe-target-health` shows each target's state and a reason code: *Target.Timeout* (cannot reach it: security group, port, app not listening), *Target.ResponseCodeMismatch* (the app answered with an unexpected status) or *Target.FailedHealthChecks*.

## 1.6 Application Load Balancer (ALB): Layer 7

**What it is.** A load balancer that understands HTTP and HTTPS.

* **Listeners and rules.** A listener (port and protocol) holds rules. Each rule has conditions (host name, URL path, header, query string, source IP, HTTP method) and an action (forward to a target group, redirect, fixed response, or authenticate through an identity provider). One ALB can serve many applications.
* **TLS termination** with certificates from AWS Certificate Manager, several certificates per listener (SNI), and a choice of TLS policy.
* **Integrations:** AWS WAF, HTTP/2, WebSockets, gRPC.
* **Headers:** it adds X-Forwarded-For (the client's address), X-Forwarded-Proto and X-Forwarded-Port, so the application must read the client IP from the header.
* **Idle timeout:** 60 seconds by default.
* **Needs two or more subnets** in different zones. It scales automatically. Its IP addresses change, so always use its DNS name. Cross-zone distribution is on.
* **Logs and metrics:** access logs to S3 (time at the balancer versus at the target, status returned by each) and CloudWatch metrics: request count, target response time, healthy and unhealthy host counts, and 4xx and 5xx counts separated into those generated by the balancer and by the target.

**Error codes.** 502: the target closed the connection or sent an invalid response. 503: no healthy targets. 504: the target did not answer within the timeout.

## 1.7 Network Load Balancer (NLB): Layer 4

**What it is.** A load balancer for TCP, UDP and TLS traffic. It does not look inside HTTP.

* **Very high performance** and low latency; handles sudden spikes.
* **Static addresses:** one per zone, and you can assign your own Elastic IPs. Useful when partners must allow-list fixed IPs.
* **Client IP preservation:** for instance targets the original source address is kept; otherwise use the proxy protocol.
* **TLS** can be terminated at the NLB or passed through.
* **Security groups** can now be attached to an NLB (originally they could not).
* **Idle timeout:** 350 seconds for TCP. **Cross-zone** distribution is off by default (turning it on adds cross-zone data charges).
* **Health checks:** TCP, HTTP or HTTPS.
* **PrivateLink:** an NLB is how you publish a service privately to other VPCs or accounts.

## 1.8 ALB or NLB

| | ALB | NLB |
| :--- | :--- | :--- |
| Layer | 7 (HTTP, HTTPS, gRPC, WebSockets) | 4 (TCP, UDP, TLS) |
| Routing | By host, path, header, query string | By port and protocol only |
| Static IPs | No (use the DNS name) | Yes, one per zone, optional Elastic IPs |
| Client IP | In the X-Forwarded-For header | Preserved at packet level (instance targets) |
| WAF | Yes | No (put WAF in front, for example at CloudFront) |
| Authentication | Built-in OIDC or Cognito actions | No |
| Idle timeout | 60 seconds default | 350 seconds for TCP |
| Best for | Web applications and APIs, microservice routing | Non-HTTP protocols, very high throughput, fixed IPs, PrivateLink |

A **Gateway Load Balancer** is a third type that inserts virtual security appliances (firewalls, inspection) into the traffic path. Combinations are common: Global Accelerator or an NLB in front for static IPs and an ALB behind for HTTP routing, or CloudFront with WAF in front of an ALB.

## 1.9 nginx on AWS

Production edge tiers frequently pair managed load balancers with Apache or nginx, making nginx a staple infrastructure interview topic.

**What it is.** A fast web server most often used as a **reverse proxy**: it accepts client connections and forwards requests to backend servers, adding TLS termination, caching, compression, rate limiting and header handling.

**Where it sits.** Typical edge: users, then CloudFront or a WAF, then an NLB or ALB, then a fleet of nginx instances (in an Auto Scaling group) or the nginx ingress controller in Kubernetes, then the application. Use nginx when you need behavior a load balancer does not give you: complex rewrites, custom rate limiting, request buffering, caching, or a uniform edge across clouds. If the ALB's features are enough, use only the ALB, because fewer components fail less.

```nginx
upstream app {
    server 10.0.1.10:8080 max_fails=3 fail_timeout=10s;   # passive health checking
    server 10.0.1.11:8080 max_fails=3 fail_timeout=10s;
    keepalive 64;                         # reuse connections to the app
}

server {
    listen 80;
    set_real_ip_from 10.0.0.0/16;         # trust the load balancer's subnets
    real_ip_header X-Forwarded-For;       # take the client IP from this header
    real_ip_recursive on;

    location / {
        proxy_pass http://app;
        proxy_http_version 1.1;
        proxy_set_header Connection '';   # required for upstream keepalive
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_connect_timeout 3s;
        proxy_read_timeout 30s;
    }
}
```

**Things worth knowing.**

* **Workers and connections.** A few worker processes each handle thousands of connections with an event loop. The practical limits are `worker_connections` and the operating system's open-file limit (ulimit); running out causes errors under load.
* **Real client IP.** Behind a load balancer every connection comes from the balancer, so configure the real-IP settings and trust only the balancer's addresses, otherwise clients can forge the header.
* **Health checks.** Open-source nginx does passive checks (it marks a server failed after errors); active checks are in the commercial version. Behind a load balancer, the balancer's health check on nginx matters more.
* **DNS caching trap.** If you proxy to a hostname (such as an internal load balancer name), nginx resolves it once at startup and keeps the old address. When addresses change, requests fail. Use the `resolver` directive with a variable in `proxy_pass` so it re-resolves.
* **Safe changes.** `nginx -t` tests a configuration; `nginx -s reload` applies it gracefully without dropping connections.
* **Observability.** The access log and error log, and the `stub_status` page for connection counts.
* **In Kubernetes.** The nginx ingress controller turns Ingress resources into nginx configuration. The community ingress-nginx project was reported to be retiring in 2026, so check its status and the alternatives (the AWS Load Balancer Controller, Gateway API implementations, or NGINX's own controller).

**Status codes you see through nginx.** 499: the client closed the connection before nginx answered. 502: nginx could not get a valid reply from the backend (down, crashed, or closed the connection). 504: the backend did not answer in time. 413: the body was larger than `client_max_body_size`. 400: a malformed request.

## 1.10 The chain, and how timeouts should line up

```text
Client --> ALB (idle timeout 60s) --> nginx (keepalive_timeout 75s; proxy_read_timeout 30s) --> app (request timeout 25s; keep-alive 120s)
```

Two rules keep chains like this debuggable:

1. **Idle connection timeouts should grow as you go inward.** If a backend closes an idle connection sooner than the component in front expects, the front component may send a request on a connection that was just closed, producing intermittent 502s. So nginx's keep-alive should be longer than the ALB's idle timeout, and the application's keep-alive longer than nginx's upstream keep-alive.
2. **Request timeouts should shrink as you go inward.** The application times out first (25 seconds), then nginx (30), then the ALB (60), so the component closest to the problem reports it with a clear error.

Also make each health check meaningful: an ALB check on nginx only proves nginx is up. Use a path that nginx forwards to the application if you want to catch application failure.

**Say it like this.** "I line up timeouts so idle timeouts grow inward and request timeouts shrink inward, and I read the 502, 503 and 504 codes to tell whether the balancer, nginx or the application failed."

## 1.11 DNS, edge and connecting networks

| Service | Plain description | Use it for |
| :--- | :--- | :--- |
| Route 53 | DNS with weighted, latency, geolocation and failover routing plus health checks | Steering users, gradual shifts, DR cutover. Remember caching: shifts are not instant |
| CloudFront | CDN with edge locations; caches content and speeds even uncacheable requests by ending TLS near the user and using AWS's backbone | Static assets, login page resources, WAF in front. Never cache per-user responses |
| Global Accelerator | Two fixed anycast IPs; routes TCP/UDP to the best healthy regional endpoint | Dynamic traffic, fast regional failover without DNS caching |
| WAF and Shield | Web firewall (managed rules, rate limits, bot and account-takeover rules) and DDoS protection | Credential stuffing defense. Roll rules out in count mode first |

**Connecting networks.** Peering connects two VPCs but is not transitive. Transit Gateway is a hub for many VPCs and on-premises links. PrivateLink shares one service privately (needs an NLB). Direct Connect is a dedicated link; a VPN is an encrypted tunnel over the internet. Plan non-overlapping address ranges.

**Limits that cause incidents.** A NAT gateway holds about 55,000 simultaneous connections to one destination (port exhaustion gives intermittent failures). The VPC DNS resolver accepts about 1,024 packets per second per network interface (busy DNS pods drop queries). Instances have bandwidth and packets-per-second allowances (visible with `ethtool -S`). Cross-zone data transfer costs money, and subnets can run out of IPs.

## 1.12 Networking depth: questions a networking-minded architect asks

**How does a pod's traffic to the internet get its source address with the VPC CNI?** Pods have VPC addresses that are not routable on the internet. By default the VPC CNI performs source NAT on the node for traffic leaving the VPC, so packets appear to come from the node's primary address; if the destination is inside the VPC (or reachable over peering or Transit Gateway), pod addresses are preserved. Traffic then goes to a NAT gateway (in private subnets), which translates to its Elastic IP. Consequences: a partner sees the NAT gateway's address, not the pod's; in-VPC services can allow-list pod security groups or ranges; and with custom networking or external SNAT settings the behavior changes, so check the configuration.

**What is MTU, and where does it bite in AWS?** MTU is the largest packet a link carries without fragmenting. Inside a VPC, instances usually support jumbo frames (about 9001 bytes), but the internet and many VPN paths are limited to about 1500 or less, and encapsulation (VPN, VXLAN overlays) reduces it further. TCP avoids problems with *path MTU discovery*: a router that cannot forward a large packet sends an ICMP message saying so, and the sender shrinks its packets. If a firewall or security group drops those ICMP messages, large packets vanish silently while small ones work (a "black hole"): logins load but uploads hang. Fixes: allow the relevant ICMP, clamp TCP segment size (MSS) at the tunnel or gateway, and set a consistent MTU across paths.

**How do pods on different nodes communicate with the VPC CNI?** Each pod gets a virtual network pair (veth) connecting it to the node, and the node has a route for each pod address pointing at that pair; for pods using secondary network cards, policy rules route their traffic out of the right card. Between nodes, the packet is an ordinary VPC packet from one pod address to another, routed by the VPC itself. There is no overlay, no encapsulation, and flow logs show pod addresses.

**How does `kube-proxy` in iptables mode balance traffic?** For each Service, it installs a chain of rules. A packet to the ClusterIP matches the Service's chain, which picks one endpoint chain using a probability match (for example 1 in 3 for the first of three endpoints, 1 in 2 for the next, then the rest), and that chain performs destination NAT to the pod address. The connection tracking table remembers the choice so replies and later packets of the same connection go to the same pod. You can inspect it with `iptables-save` and look for `KUBE-SVC` and `KUBE-SEP` chains. At thousands of Services these rule lists get long and slow to update, which is why IPVS or eBPF dataplanes are used at scale.

**What does an NLB do with flows, and why does that matter?** It hashes the connection's identifying values (source and destination address and port, protocol) to pick a target, so every packet of one connection goes to the same target (a "flow hash"). Different connections spread out, but a single very large connection never splits across targets. With client IP preservation, targets see the real source address; with the same instance as both client and target, hairpin traffic may not work as expected, which is a known gotcha.

**How does BGP show up with Direct Connect?** The link carries a BGP session over which AWS advertises the VPC's prefixes and your side advertises on-premises prefixes. You control which path is preferred using attributes such as local preference or AS path prepending (making one path look longer), and you use a second link (or a VPN) for backup. Failure detection: BGP timers are slow by default, so use BFD (bidirectional forwarding detection) for sub-second detection. Route limits and overlapping address ranges are the usual pitfalls.

**Why does DNS sometimes fail only under load, and what is the TCP angle?** DNS uses UDP; responses too large for UDP fall back to TCP. In Linux, parallel UDP lookups through the connection tracking table can race and drop packets, causing multi-second stalls. A node-local DNS cache that talks to the cluster DNS over TCP avoids this, and also reduces load on the VPC resolver.

**Security group, network policy, security group for pods: how do they differ?** Security groups are AWS's firewall on network interfaces (cloud-level, stateful, allow-only); network policies are Kubernetes's firewall between pods (selected by labels, enforced by the CNI); security groups for pods attach AWS security groups to individual pods (so a pod can be the *only* thing allowed to reach a database). Use network policies for pod-to-pod rules and security groups at the boundary with AWS resources.

## 1.13 IAM in plain terms

**What it is.** IAM decides who can do what in AWS. A **role** is an identity with no permanent password that a person, service or server temporarily assumes, receiving short-lived credentials. **Policies** are documents that allow or deny actions on resources.

**How a decision is made.** Everything is denied by default; an explicit allow is needed; an explicit deny anywhere always wins. Organization guardrails (service control policies) and permission boundaries cap what identity policies can grant, so the effective permission is the overlap of everything that applies.

**Cross-account access.** The target account creates a role whose *trust policy* names who may assume it; the caller is granted permission to assume it. No long-lived keys are involved.

**Workloads.** Servers use instance roles; Kubernetes pods use IAM roles for service accounts or EKS Pod Identity, so each application gets only what it needs.

**Mistakes to avoid.** Wildcard permissions, letting someone pass a powerful role to a service (privilege escalation), and long-lived access keys. **Tools:** CloudTrail records every API call; Access Analyzer finds unintended access; the policy simulator explains denials.

## 1.14 Compute and storage essentials, explained

### EC2 instances and instance families

**What it is.** An EC2 instance is a virtual server. Its type name tells you what it is built for. In `m5.large`, the letter is the **family** (m is general purpose, c is compute-heavy, r is memory-heavy, i has fast local storage, t is burstable), the number is the hardware **generation** (newer is usually faster and cheaper per unit of work), an optional letter such as `g` means Graviton (ARM-based chips), and `large` is the **size**.

**Why it matters.** The wrong family wastes money or causes a bottleneck: a database wants memory and fast disk (r or i families), a web tier usually wants compute (c or m). Newer generations and Graviton typically give better price and performance once your software supports them.

**Say it like this.** "I choose the family by the bottleneck: memory for caches and databases, compute for stateless request handling, and I move to newer generations or Graviton for cost once the software supports it."

### Nitro: why instance size has hard limits

**What it is.** Nitro is AWS's modern virtualization design. It moves networking, storage and security work onto dedicated cards, so almost all of the server's CPU goes to your workload.

**Why it matters for troubleshooting.** Every instance size has fixed limits for network bandwidth, packets per second, and storage (EBS) bandwidth. A fast disk volume attached to a small instance is still limited by the instance's disk bandwidth. When counters such as "allowance exceeded" (visible with `ethtool -S eth0`) are rising, the instance, not your code, is dropping packets, and the answer is a bigger size or a redesign.

### Burstable instances and CPU credits

**What it is.** T-family instances (t3, t4g) are cheap because you pay for a low baseline of CPU. While idle they *earn* credits; when busy they *spend* them. Think of a phone data plan: fine until the allowance runs out.

**Why it matters.** When credits run out, in standard mode the instance is throttled to its baseline and latency jumps with no traffic change; in unlimited mode (the default on newer T types) it keeps full speed but you pay extra for the surplus. Either way it is a surprise. Use burstable types for development or light workloads, fixed-performance families for steady production load, and alert on the credit balance.

### Auto Scaling Groups (ASGs)

**What it is.** An Auto Scaling Group keeps a fleet of identical instances at the right size. You define a **launch template** (the recipe: image, instance type, security groups, startup script) and minimum, desired and maximum counts. The group replaces unhealthy instances and adds or removes instances as load changes.

**The parts people ask about, each explained.**

* **Health checks: EC2 versus ELB.** By default the group only checks that the instance is running. That misses the common failure where the machine is up but the application is broken. With **ELB health checks** enabled, the group also replaces instances the load balancer marks unhealthy.
* **Scaling policies.** *Target tracking* works like a thermostat: "keep average CPU near 50 percent," and AWS adds or removes instances to hold it. *Step scaling* uses alarms with steps (above 70 percent add two, above 90 percent add four), giving finer control but needing tuning. *Scheduled* scaling adds capacity at known times such as a morning peak.
* **Cooldown and warmup.** After scaling, the group waits before scaling again so it does not flap up and down. Warmup tells it how long a new instance needs before it counts toward the metrics.
* **Instance refresh.** A rolling replacement of every instance, used to roll out a new image or launch template. You set a minimum healthy percentage so capacity does not drop too far during the rollout.
* **Lifecycle hooks.** They pause an instance as it launches or terminates so your automation can act first: register it in a service catalog, finish draining connections, upload logs. Without a hook, an instance can be terminated mid-request.
* **Warm pools.** Pre-initialized instances kept stopped (or hibernated) and ready, so scale-out takes seconds instead of the minutes needed to boot and configure a new instance. Useful when startup is slow.

**Say it like this.** "For a stateless tier I use an ASG with ELB health checks, target tracking on a request-based metric, lifecycle hooks to drain connections, and instance refresh with a minimum healthy percentage for image rollouts. For slow-starting apps a warm pool shortens scale-out."

### Spot instances

**What it is.** Spare AWS capacity sold at a steep discount, with the catch that AWS can take it back with a two-minute warning. It suits fault-tolerant work (batch jobs, CI runners, stateless workers) and is wrong for anything that cannot lose a node suddenly. Good practice: diversify across several instance types and zones, handle the interruption notice (drain and checkpoint), and keep a baseline of on-demand capacity.

### AMIs and Packer (golden images)

**What it is.** An AMI is a saved disk image used to launch instances. Packer builds AMIs automatically from a script. A golden-image pipeline builds a hardened, patched image regularly, tests it, and publishes it.

**Why it matters.** It enables *immutable infrastructure*: instead of logging into servers to patch them, you build a new image and replace the servers. That rolls out faster, rolls back more easily, and avoids drift (servers slowly becoming different from each other). The trade-off is build time and pipeline upkeep. Configuration tools such as Chef or Ansible still fill gaps for settings applied at boot and for older fleets.

### IMDSv2 (the instance metadata service)

**What it is.** Every EC2 instance can ask a special local address (169.254.169.254) about itself, including temporary credentials for its IAM role. Version 1 answers any simple request. Version 2 requires first obtaining a session token with a special request and sending it in a header.

**Why it matters.** If an attacker tricks an application into making a request on their behalf (server-side request forgery), version 1 lets them fetch the role's credentials. Version 2 blocks most such attacks, and a hop limit of one stops containers on the node from reaching it. Require IMDSv2 on all instances and set the hop limit to one.

### EBS (block disks for EC2)

**What it is.** EBS volumes are network-attached disks for EC2. A volume lives in one availability zone, so it cannot be attached to an instance in another zone (a Kubernetes pod that needs it must be scheduled in that zone).

**The three performance numbers.** *IOPS* is operations per second (many small reads and writes, typical of databases). *Throughput* is megabytes per second (large sequential reads, typical of scans and backups). *Latency* is time per operation. A database cares about IOPS and latency; a log pipeline cares about throughput.

**Volume types.** gp3 is the general-purpose default: 3,000 IOPS and 125 MB per second baseline, which you can raise independently of size. io2 is for demanding databases that need high, consistent IOPS and low latency. The older gp2 ties IOPS to size and uses a burst bucket that can run dry.

**Two gotchas.** The *instance* has its own cap on disk bandwidth, so a fast volume on a small instance is still limited. And a volume created from a snapshot loads data lazily from S3 in the background, so first reads of each block are slow until warmed (fast snapshot restore avoids this): a restore drill can "work" and still perform badly at first.

### S3 (object storage)

**What it is.** Storage for objects (files) addressed by key, extremely durable and effectively unlimited, with strong read-after-write consistency (a new object is visible immediately). It is where backups, logs, Terraform state and artifacts live. Performance scales with request rate per key prefix; when you hit limits you get 503 SlowDown responses, and the answer is to spread keys across prefixes and retry with backoff. Lifecycle rules move or delete old objects to save cost, versioning protects against accidental deletes, and replication copies data to another region. For security: block public access, encrypt, and restrict access by role.

### RDS (managed relational databases)

**What it is.** AWS runs the database for you (provisioning, patching, backups, failover). You still own the schema, queries, sizing and parameter settings.

**Multi-AZ.** A standby copy runs in another zone, kept in sync. You cannot read from it. If the primary fails, RDS switches to the standby and updates the DNS name, which usually takes on the order of one to two minutes. Applications must reconnect, so retries and short DNS caching matter.

**Read replicas.** Asynchronous copies for scaling reads. They can lag behind, so reads can be slightly stale. They can also serve as a disaster recovery copy in another region.

**Other concepts.** Parameter groups (database settings you control), Performance Insights (shows which queries and waits use database time), storage autoscaling, automated backups with point-in-time recovery (restore to any moment in the retention window), maintenance windows, and Blue/Green deployments (Part 11).

**Compute questions to expect.**

* *A service is slow only sometimes, and CPU looks high but the app does little.* Check steal time and the credit balance on burstable types, then iowait (waiting on disk), then a runaway agent or log shipper.
* *Scale-out failed during a spike.* API throttling, service quotas, no capacity of that instance type in the zone, no free IP addresses in the subnet, or slow boot. Fix with pre-provisioning or warm pools, multiple instance types, quota monitoring and generous subnets.
* *How do you roll out a new image safely?* Build and test an AMI, update the launch template, run an instance refresh with a high minimum healthy percentage, watch error rate and latency, and roll back by refreshing back to the old template. Do it in one cell first.
* *What happens to my application during a Multi-AZ failover?* The connection drops, the DNS name moves to the standby, and the app reconnects after a short outage. Good apps retry with backoff, re-resolve DNS and use short timeouts; an RDS Proxy can hold connections and shorten the impact.

## 1.15 Troubleshooting AWS and network traffic

**Method: work from the user toward the application, cheapest check first.**

1. Define the symptom: which source, destination, port, since when, always or sometimes. What changed?
2. **DNS:** does the name resolve to the right address? (`dig name`)
3. **Route:** is there a path? Route tables, peering or Transit Gateway, overlapping ranges. Reachability Analyzer evaluates the configuration.
4. **Filters:** security groups and NACLs in both directions (remember NACLs are stateless).
5. **Listener and port:** `nc -vz host port`; `ss -ltnp` on the server.
6. **Load balancer and targets:** target health and reason code; did the balancer or the target generate the error?
7. **Application.**
8. **Where does the time go?** `curl -s -o /dev/null -w '%{time_namelookup} %{time_connect} %{time_appconnect} %{time_starttransfer} %{time_total}' URL`. Slow connect means the network; slow first byte means the server.
9. **Packets when needed:** `tcpdump` (retransmits, resets), `mtr` (loss per hop), VPC Flow Logs (ACCEPT or REJECT per connection; REJECT points to a security group or NACL).

**Scenarios, each in one breath.**

* **EC2 unreachable:** status checks (system versus instance), security group, NACL both ways, route to the internet gateway or Session Manager, key pair, full disk or boot failure (console output).
* **S3 Access Denied:** several layers each can say no: the caller's IAM policy, bucket policy, organization policy, permission boundary, the KMS key policy (if encrypted), VPC endpoint policy, Block Public Access. Find the real caller (`aws sts get-caller-identity`) and read the CloudTrail error.
* **Unhealthy targets or 503:** `describe-target-health` reason code; security group from the balancer, health check path and port, app not listening, health check grace period too short.
* **RDS connection fails:** `nc -vz endpoint 3306` separates network from authentication. Timeouts mean security groups or routing; refusals mean credentials, connection limits, TLS or a failover in progress (re-resolve DNS).
* **Intermittent 502:** idle timeout mismatch between hops, errors during deploys (deregistration delay, graceful shutdown), target resource exhaustion.
* **Intermittent timeouts to an external API from private subnets:** NAT port exhaustion first, then DNS drops.
* **ASG not scaling or instances terminating immediately:** read `describe-scaling-activities` (capacity, quota, bad launch template, missing KMS permission for encrypted volumes); a health check failing before the app is ready (extend the grace period).
* **Bill spike:** Cost Explorer by service and usage type; usual causes are NAT data processing, cross-zone transfer, log ingestion, forgotten test environments and large snapshots.
* **Small requests work, large ones hang:** MTU or fragmentation (VPN, peering).
* **Logins slow for one region:** time each phase from there; slow connect and TLS with normal server time means distance, so end TLS at an edge near them and cut sequential calls.

---

## 1.16 More AWS troubleshooting scenarios

1. **One availability zone is impaired.** Confirm scope with health dashboards and your own metrics; shift traffic away (a load balancer zonal shift where supported, or remove the zone's targets); cordon and drain nodes; watch capacity and quotas in the surviving zones and the database failover; avoid actions that depend on the impaired zone's control plane; communicate; review after.
2. **A database failover happened but applications did not recover.** Clients cached the old DNS address or held dead connections. Use short DNS caching, connection pools that validate and retry, timeouts, and RDS Proxy; test failovers regularly.
3. **A mass restart caused KMS or Secrets Manager throttling.** Thousands of pods all fetched secrets or keys at once and hit API limits. Cache secrets and data keys, stagger restarts, increase refresh intervals, and use an operator that fetches once and distributes.
4. **Route 53 failover did not trigger, or flapped.** Health check checks the wrong thing or from too few locations, thresholds too tight, or the record's TTL kept clients on the old address. Use meaningful health checks, calculated or multi-signal checks, sensible thresholds, and consider Global Accelerator or routing controls for faster cutover.
5. **A TLS certificate expired.** An ACM certificate failed to renew because the DNS validation record was removed or the certificate was not in use, or an in-cluster certificate manager failed. Alert on days to expiry (ACM publishes a metric), keep validation records under change control, and test renewals.
6. **An IAM or organization policy change broke production.** Find the change in CloudTrail, identify the denied action in the error, revert (or add the specific allow), and prevent with staged policy rollout, the policy simulator, and a break-glass role.
7. **An access key leaked, or a workload is compromised.** Contain first: disable or rotate the credential, isolate the instance or pod (security group, network policy, cordon), preserve evidence (snapshots, logs), review CloudTrail for what the credential did, look at GuardDuty findings, rotate anything it could reach, then root cause and prevention (short-lived credentials, least privilege).
8. **An EBS volume is stuck attaching, or pods report the volume is already attached elsewhere.** After a node failure the volume has not yet detached from the old instance. Confirm the old node is truly gone, check volume attachments, wait for or force the detach, and keep the pod's zone matched to the volume.
9. **A scale event fails because of a quota.** vCPU, network interface, Elastic IP or load balancer limits. Monitor quota usage, raise limits ahead of known events, and use multiple instance types and zones.
10. **A cost spike from NAT gateway data processing.** Heavy S3 or container registry traffic going through NAT. Add a gateway endpoint for S3 and interface endpoints for the registry, and review cross-zone traffic.
11. **Connectivity works one way only between VPCs.** A missing return route or an asymmetric path through peering or Transit Gateway, or a security group or network ACL blocking the reply. Check route tables on both sides and use Reachability Analyzer.
12. **Monitoring exporters are throttled by CloudWatch or the bill rose.** Too many metric queries or high-cardinality custom metrics. Use metric streams instead of polling, reduce dimensions, and lengthen polling intervals.
13. **A load test shows 503 errors from the ALB at the start of a sharp ramp.** The load balancer scales with load and a very steep ramp can outrun it. Ramp more gradually, use the load balancer's capacity reservation or ask AWS to pre-scale for known events, and check target capacity too.
14. **S3 returns 503 SlowDown.** A hot key prefix or request spike. Spread keys, add retries with backoff and jitter, and use caching.

---

# Part 2: Terraform

## 2.1 Configuration, state, plan and reality are four different things

Here are the four core Terraform concepts defined precisely:

| Term | What it is | Where it lives |
| :--- | :--- | :--- |
| **Configuration** | The `.tf` files you write: what you want | Git |
| **State** | Terraform's record of what it created: which real resource matches each block, plus its IDs and attributes | A state file, stored remotely (for example in S3) |
| **Real infrastructure** | What actually exists in AWS | AWS |
| **Plan** | The computed list of changes needed to make reality match the configuration | Printed (or saved) on demand |

Analogy: the configuration is the architect's drawing; the state is the building inventory with serial numbers; the real infrastructure is the building; the plan is the list of work orders.

**How they connect.** `terraform plan` reads the configuration, loads the state, refreshes it by asking AWS what exists now, and compares everything. `apply` carries out the changes and writes the new state. Each *root module* (the folder you run Terraform in) has its own configuration and its own state, so when people say "split the state" they mean "split into separate root modules, each with a state file", which also limits the damage of a mistake.

## 2.2 How Terraform talks to AWS (the first-time walkthrough)

Terraform runs on your laptop or a CI server and calls AWS APIs over HTTPS using credentials you give it. It does not keep AWS credentials in your Terraform files or state.

1. **Give your shell AWS credentials.** Best: a short-lived session, for example `aws configure sso` then `aws sso login --profile myprofile` and `export AWS_PROFILE=myprofile`. Alternatives: environment variables (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`), a profile in `~/.aws/credentials` or `~/.aws/config`, an instance or container role (when Terraform runs on EC2, ECS or Kubernetes), or, in CI, an OIDC login that assumes a role. Confirm who AWS thinks you are with `aws sts get-caller-identity`.
2. **Write a provider block and a backend block.**

```hcl
terraform {
  backend "s3" {
    bucket  = "org-tf-state-prod"
    key     = "cells/us-east-1/cell-001/terraform.tfstate"
    region  = "us-east-1"
    encrypt = true
    # locking: DynamoDB table (dynamodb_table = "tf-locks") or, on newer versions, use_lockfile = true
  }
}

provider "aws" {
  region = "us-east-1"
  assume_role {
    role_arn = "arn:aws:iam::111111111111:role/terraform-cell"   # work in another account
  }
}
```

3. **`terraform init`.** Reads the backend block, connects to the S3 bucket using credentials, and downloads the provider plugins from the Terraform registry (the AWS provider is a program that translates your resources into AWS API calls). It records provider versions in `.terraform.lock.hcl`.
4. **`terraform plan`.** Downloads the state file from S3 (it needs `s3:ListBucket` on the bucket and `s3:GetObject` on the key), then the provider calls AWS describe and get APIs using its credentials to refresh, then it compares and prints the plan.
5. **`terraform apply`.** Takes the lock (a DynamoDB item, or a small lock file in S3, which needs `s3:PutObject` and `s3:DeleteObject`), makes the AWS API calls to create or change resources, writes the updated state back to S3, and releases the lock.

**Two separate sets of credentials.** The S3 backend and the AWS provider each authenticate on their own. By default both use the same chain, but the backend block can name its own profile or role (so the state bucket can live in a shared "tools" account while the provider assumes a role in the workload account). If `init` fails with access denied, the problem is the backend's credentials; if `plan` fails after loading state, it is the provider's.

**How the AWS provider finds credentials (roughly in this order).** Settings in the provider block (avoid hard-coding keys), then environment variables, then the shared credentials and config files and profiles (including SSO), then web-identity or container credentials, then the EC2 instance profile. With `assume_role`, it first uses the base credentials and then switches to the role.

**Where credentials are "saved."** Not by Terraform. They live in your environment, in `~/.aws`, or are issued by a role at run time. The `.terraform/` folder caches providers and backend settings (no AWS keys). Never commit `.terraform/`, state files, or `.tfvars` files that contain secrets. The state itself can contain secrets (resource attributes), so encrypt the bucket and restrict access.

**The bootstrap problem.** The S3 bucket must exist before Terraform can use it as a backend. Create it once by hand or with a tiny bootstrap configuration using local state, then migrate with `terraform init -migrate-state`. Turn on versioning (so you can recover a damaged state), encryption and Block Public Access, and limit who can read or write it.

**Say it like this.** "Terraform runs wherever I run it and calls AWS with short-lived credentials from my SSO session, an assumed role or CI's OIDC login. The backend uses its own credentials to read and write state in S3 with locking, and the provider uses its credentials to refresh and change real resources."

## 2.3 The core concepts in five lines

* **Provider** = plugin for a platform (AWS, Kubernetes, Grafana). **Resource** = something Terraform creates. **Data source** = reads something that exists.
* **Variables** are inputs, **locals** are computed names inside a module, **outputs** are results other code can use. Variable precedence: defaults, then `TF_VAR_` environment variables, then `terraform.tfvars`, then `*.auto.tfvars`, then `-var` and `-var-file` (last wins).
* **count versus for_each:** count tracks copies by position (removing one from the middle shifts the rest and may recreate them); for_each tracks by stable key (only the removed one changes). Prefer for_each.
* **lifecycle:** `create_before_destroy`, `prevent_destroy` (seatbelt for databases), `ignore_changes` (fields managed elsewhere, like an ASG's desired count).
* **Refactoring:** `moved` blocks, `import` blocks, `state mv`. Back up state first and require a clean plan afterwards.

## 2.4 Modules, environments, workspaces and cells

**A module** is a folder of Terraform code with inputs and outputs, reusable like a function. **A root module** is where you run Terraform; it has its own backend and state and calls child modules (which have no state of their own).

**What goes in modules (three layers).**

| Layer | Examples |
| :--- | :--- |
| Building blocks | Encrypted S3 bucket, standard IAM role, security group with safe defaults |
| Domain modules | network (VPC, subnets per zone, NAT, endpoints), eks-cluster, mysql-db (instance, parameter group, backups, replicas), redis, edge (load balancers, WAF, certificates, DNS), observability (collector config, dashboards, alerts) |
| Blueprint | `cell`: composes the domain modules and wires outputs to inputs |

```text
terraform-modules/            (released with version tags)
  modules/ network  eks-cluster  mysql-db  redis  edge  observability  cell
live/                         (the desired state of every real environment)
  manifests/ profiles.yaml  envs/prod.yaml  cells/cell-101.yaml
  stacks/cell/                one generic root module reused by every cell
```

**Environments: three ways.**

| | Folder per environment or cell | Workspaces | Generated roots (Terragrunt or a generator) |
| :--- | :--- | :--- | :--- |
| Clear what you will change | Yes (the path says it) | Weak (hidden current workspace) | Yes |
| Different accounts and permissions | Easy | Awkward (one backend and credentials) | Easy |
| Risk of applying to the wrong target | Low | Higher | Low |
| Best use | Production environments and cells | Short-lived test copies | Large fleets of similar stacks |

**Recommended for cell-based architectures:** a versioned modules repository, plus a live repository with **one root module per cell, each with its own state**. Cells then have small plans, a small blast radius, parallel pipelines, and per-cell approval rules (production versus federal). A module upgrade is a version change applied in waves (canary cell first). Use workspaces only for throwaway copies.

**Data-driven cells (people provide only sizes and ranges).** Keep *what* separate from *how*. Three layers of data are merged, later layers winning: **profiles** (t-shirt sizes), **environment defaults**, **cell overrides**.

```yaml
# manifests/profiles.yaml
profiles:
  small:  { db_instance_class: db.r6g.xlarge,  asg_min: 3, asg_max: 12 }
  large:  { db_instance_class: db.r6g.8xlarge, asg_min: 9, asg_max: 36 }

# manifests/envs/prod.yaml
account_id: '111111111111'
defaults: { multi_az: true, backup_retention_days: 14 }

# manifests/cells/cell-101.yaml   <- all a cell owner writes
cell_id: cell-101
env: prod
region: us-east-1
size: large
cidr: 10.101.0.0/16
overrides: { asg_max: 40 }
```

```hcl
variable "cell_id" { type = string }

locals {
  cell     = yamldecode(file("${path.module}/../../manifests/cells/${var.cell_id}.yaml"))
  env      = yamldecode(file("${path.module}/../../manifests/envs/${local.cell.env}.yaml"))
  profiles = yamldecode(file("${path.module}/../../manifests/profiles.yaml")).profiles

  # precedence: profile < environment defaults < cell overrides
  settings = merge(local.profiles[local.cell.size], try(local.env.defaults, {}), try(local.cell.overrides, {}))
}

module "cell" {
  source   = "git::https://git.example.com/platform/terraform-modules.git//modules/cell?ref=v3.2.0"
  cell_id  = local.cell.cell_id
  region   = local.cell.region
  cidr     = local.cell.cidr
  settings = local.settings
}
```

Inside the cell module the sizes become real values, and subnets are derived from the one CIDR so owners never write them:

```hcl
variable "settings" {
  type = object({
    db_instance_class = string
    asg_min           = number
    asg_max           = number
    multi_az          = optional(bool, true)
  })
}

locals {
  azs             = slice(data.aws_availability_zones.available.names, 0, 3)
  public_subnets  = [for i, az in local.azs : cidrsubnet(var.cidr, 8, i)]
  private_subnets = [for i, az in local.azs : cidrsubnet(var.cidr, 8, i + 10)]
  data_subnets    = [for i, az in local.azs : cidrsubnet(var.cidr, 8, i + 20)]
}
```

**Running it per cell.** A backend block cannot use variables, so the pipeline passes the state location at init: `terraform init -backend-config="key=cells/cell-101/terraform.tfstate"` then `terraform apply -var cell_id=cell-101`, looping over manifests wave by wave.

**"Importing" modules from a manifest.** You cannot: a module's `source` must be a literal string, not a variable. A manifest drives *values*, not which module or version loads. Options: pin the version in the root (simplest; an upgrade is a version bump in waves); use Terragrunt or a small generator when different cells must run different versions; or use `for_each` on the module block for many cells in one root (one shared state, and no per-cell provider region, so only for small dev sets). Use YAML if portals and scripts also write manifests; use `.tfvars` if only Terraform reads them.

**Guardrails.** Policy checks keep overrides within bounds (for example a maximum ASG size), CODEOWNERS approvals for production overrides, and a CI check that CIDRs do not overlap.

## 2.5 Questions you will likely get

* **What happens if a plan wants to destroy and recreate the production database?** Stop. Find what "forces replacement", revert or avoid it, and protect stateful resources with `prevent_destroy`, deletion protection, snapshots and a policy check.
* **The state lock is stuck.** Confirm no apply is running (check CI and the lock owner and time), then `terraform force-unlock ID`. Find out why the job died.
* **Someone changed infrastructure by hand.** `plan` shows drift. Decide whether to revert or update the code; prevent repeats with restricted console access, drift jobs and CloudTrail alerts.
* **An apply failed halfway.** Terraform recorded what succeeded; fix the cause and run again.
* **Secrets?** Never hard-code. Reference a secrets manager, mark values `sensitive` (hides output but not state), encrypt and restrict the state.
* **CI/CD for Terraform?** On pull request: format, validate, lint, security and policy scans, then `plan` posted for review. On merge: apply the saved plan with an approval for production, one apply per state at a time, least-privilege role. A scheduled plan-only job detects drift.
* **Replacing `taint`?** `terraform apply -replace=ADDRESS`. **Refresh?** Use a refresh-only plan.
* **Roll a module change to 100 cells?** Test in a throwaway account, release a candidate, apply to staging then a canary cell, review each plan for deletions, check health between waves, and keep the previous version to roll back.
* **Terraform versus CloudFormation (an architect will likely know both).** CloudFormation is AWS-only; AWS holds the state; stacks roll back automatically on failure; change sets preview changes; StackSets handle many accounts; new AWS features appear quickly. Terraform is multi-cloud with a much larger ecosystem and a richer language, shows a plan, and works with Kubernetes, Grafana and Splunk, but you must manage state and there is no automatic rollback. Pick by scope: AWS-only teams can be happy with CloudFormation; a multi-cloud platform team usually wants Terraform. Know that the AWS CDK generates CloudFormation from code.

---

## 2.6 Terraform question bank, with explained answers

The answers are written so you can explain the reasoning, not recite a phrase.

### Basics

**What is Terraform, and why use infrastructure as code?** Terraform lets you describe infrastructure (networks, servers, databases, permissions) in text files and creates it for you. Because the description lives in version control, changes are reviewed like code, environments can be recreated identically, mistakes can be rolled back, and nothing depends on one person's memory of console clicks.

**How does it differ from CloudFormation, Ansible and Pulumi?** CloudFormation is AWS-only and managed by AWS (AWS holds the state, and stacks roll back automatically on failure); Terraform works across many providers (AWS, GCP, Kubernetes, Grafana, Splunk) and shows a plan, but you manage the state yourself. Ansible is mainly configuration management (installing software, changing settings on servers) and is procedural, while Terraform is declarative and focused on creating infrastructure. Pulumi does the same job as Terraform but lets you write in a general-purpose language.

**What do the main commands do?** `init` prepares a folder (downloads providers, configures the backend where state is stored). `validate` checks syntax. `fmt` formats files. `plan` shows what would change without changing anything. `apply` makes the changes. `destroy` deletes everything the configuration manages. `output` prints output values. `show` displays state or a saved plan.

**What is a provider?** A plugin that knows how to talk to one platform's API. Terraform core cannot create an EC2 instance; the AWS provider does. `init` downloads providers, and the lock file (`.terraform.lock.hcl`) records exact versions and checksums so every machine uses the same ones. Commit the lock file.

**Variables, locals, outputs?** Variables are inputs; locals are named values computed inside a module to avoid repetition; outputs are values a module exposes to its caller or the command line. When several sources set a variable, later ones win: defaults, then `TF_VAR_` environment variables, then `terraform.tfvars`, then `*.auto.tfvars`, then `-var` and `-var-file` flags.

**Data source versus resource?** A resource is something Terraform creates and manages. A data source only reads information about something that already exists (the latest AMI, an existing VPC) so you can reference it.

**How are dependencies handled?** Terraform builds a graph. If one resource refers to another's attribute (a server using a subnet's ID), the order is inferred. When there is a hidden relationship Terraform cannot see, use `depends_on`, sparingly, because it can force unnecessary replacements.

**count versus for_each?** Both create several copies. `count` tracks copies by position, so removing an item from the middle of a list shifts everything after it and can destroy and recreate resources. `for_each` tracks copies by a stable key, so only the removed item changes. Use `for_each` for collections and `count` for simple on/off switches (`count = 0` or `1`).

**Dynamic blocks and useful functions?** A *dynamic block* generates repeated nested blocks from a collection, such as one security group rule per entry in a list:

```hcl
resource "aws_security_group" "app" {
  name = "app"
  dynamic "ingress" {
    for_each = var.allowed_ports            # for example [80, 443]
    content {
      from_port   = ingress.value
      to_port     = ingress.value
      protocol    = "tcp"
      cidr_blocks = ["10.0.0.0/16"]
    }
  }
}
```

Frequently used functions: `merge` (combine maps, often tags), `lookup` (read a map with a default), `templatefile` (render a file with variables), and `cidrsubnet`, which carves a smaller network from a larger one: `cidrsubnet("10.0.0.0/16", 8, 3)` gives `10.0.3.0/24`.

### Intermediate

**Remote state and locking.** Use a remote backend (S3 with encryption and versioning, or Terraform Cloud) so the team shares one state, and enable locking so only one apply runs at a time. Classic S3 setups lock with a DynamoDB table; newer Terraform versions can lock in S3 itself, so check your version. Restrict who can read the state.

**Can one configuration read another's outputs?** Yes, through the `terraform_remote_state` data source, or better by reading shared values from a parameter store or by looking resources up with data sources. Remote-state reads couple configurations tightly and need read access to the other state.

**Workspaces: when do they fall short?** Workspaces give one configuration several state files. They are convenient for identical copies but share the same code, backend and credentials, so it is easy to apply to the wrong one, and they do not model different accounts and approval rules. For environments with different access and risk, use separate directories or accounts (Part 2).

**Bringing existing infrastructure under Terraform.** With `terraform import` (older, state only) or an `import` block in the configuration (newer, reviewable in a plan). Newer versions can draft the configuration (`plan -generate-config-out=file.tf`) which you then clean up. You must still write or review the configuration, and any difference between your code and reality shows up in the next plan.

**Provisioners.** They run commands or scripts when a resource is created. They break the declarative model, because Terraform cannot see what the script did, and failures leave things half-done. Prefer machine images, cloud-init or a configuration tool.

**Drift.** Run `terraform plan` (which refreshes real state and compares) or a refresh-only plan. Decide whether to revert the manual change or update the code, and prevent repeats with restricted console access and audit alerts.

**What replaced `terraform taint`?** The `-replace` option: `terraform apply -replace=aws_instance.web` forces that resource to be recreated in one reviewable step.

**`-target`.** It limits a plan or apply to specific resources. It is a break-glass tool, not a routine one, because skipping part of the graph can leave the rest out of sync.

**The lifecycle block.** `create_before_destroy` (build the replacement first), `prevent_destroy` (refuse any plan that deletes it), `ignore_changes` (skip fields managed elsewhere, such as an autoscaling group's desired count), and `replace_triggered_by`.

**Zero-downtime changes.** Use immutable replacement: a new launch template or image version, then an Auto Scaling group instance refresh, or `create_before_destroy` for resources that must always exist. For bigger changes, build a second copy and shift traffic with weighted target groups or weighted DNS, then retire the old one.

**Multiple accounts or regions in one configuration.** Define several provider blocks with aliases, each assuming a different role or region, and pass the right provider to each resource or module:

```hcl
provider "aws" { region = "us-east-1" }
provider "aws" {
  alias  = "dr"
  region = "us-west-2"
}
resource "aws_s3_bucket" "backup" {
  provider = aws.dr
  bucket   = "example-backup-dr"
}
```

**Secrets.** Never hard-code them. Mark variables and outputs `sensitive` (hides them in plan output but they are still stored in state), read secrets at runtime from a secrets manager, and encrypt and restrict the state.

**CI/CD integration.** On every pull request: format, validate, lint, security and policy scans, then `plan` posted for review. On merge, apply the saved plan (`-out`) so what runs is exactly what was reviewed, with an approval for production, one apply per state at a time. Add a scheduled plan-only job for drift. Tools: Atlantis, Terraform Cloud, Spacelift, or GitHub Actions or Jenkins pipelines.

**Policy as code and testing.** Sentinel or Open Policy Agent block unsafe plans (no public buckets, required tags). Test with `validate`, linting, policy scans, the built-in test framework (newer versions) and Terratest in a throwaway account.

### Advanced

**Terraform Cloud and Enterprise versus open source.** Open source is the command-line tool; you provide state storage, locking and pipelines. Terraform Cloud adds hosted remote state, run management, access control, version-control integration and policy checks. Enterprise is the self-hosted version.

**Module versions and provider upgrades.** Pin modules to released versions with semantic versioning, so a major number signals a breaking change. Pin providers with constraints and the lock file; to upgrade, change the constraint and run `terraform init -upgrade`, read the changelog, run plans against several environments, and roll out one environment at a time.

**State commands.** `state list` and `state show` inspect; `state mv` renames or moves a resource without destroying it; `state rm` stops managing something without deleting it; `state pull` and `push` download or replace state. They edit Terraform's memory directly, so back up state first and confirm with a plan afterward. Moving between backends uses `init -migrate-state`.

**State lost or corrupted.** Restore a previous version from the versioned bucket. If none exists, rebuild by importing each resource, which is slow, and shows why versioning, backups and access control on the state bucket are essential.

**Managing EKS with Terraform.** Terraform creates the cluster, node groups or Karpenter, add-ons and the IAM roles for service accounts. The Kubernetes and Helm providers can also deploy inside the cluster, but they depend on the cluster existing and being reachable, which makes a single combined configuration fragile, so many teams use a separate state for in-cluster resources and let a pipeline or GitOps manage applications.

**When to write a custom provider.** When you must manage something with no provider, such as an internal API. Providers are written in Go with HashiCorp's plugin framework (define resources, implement create, read, update, delete). Often an existing provider, a pipeline script, or a Kubernetes operator is a simpler choice.

**Registry, Terragrunt, OpenTofu.** The registry hosts public providers and modules. Terragrunt is a wrapper that reduces repetition across many configurations. OpenTofu is an open-source fork created after HashiCorp changed Terraform's license; it is largely compatible, and your organization's policy decides which to use.

### Troubleshooting Terraform

Start with the error message, then `terraform plan` to see current differences. Turn on detailed logging with `TF_LOG=DEBUG` (and `TF_LOG_PATH`). Common failures:

* **Authentication or permission errors:** confirm which identity Terraform is using and that its role allows the action; check for an explicit deny from an organization policy.
* **Resource already exists:** created outside Terraform or by an earlier partial apply; import it or remove the duplicate.
* **Error acquiring the state lock:** confirm no apply is running (check CI and the lock owner and time), then `terraform force-unlock ID`; find out why the job died.
* **Quota or limit exceeded:** request a quota increase or lower `-parallelism` if the cloud API is throttling.
* **Cycle error:** two resources depend on each other; break the loop (for example, separate security group rule resources instead of inline rules that reference each other).
* **Unexpected changes in the plan:** read the diff for the attribute; check provider version changes, defaults that changed, and drift.
* **Apply failed halfway:** Terraform recorded what succeeded; fix the cause and run again.
* **Plan wants to destroy a production database:** stop; find what "forces replacement"; revert, ignore the field if something else manages it, or build a new resource from a snapshot; protect with `prevent_destroy`, deletion protection and a policy check.

# Part 3: Kubernetes fundamentals

## 3.1 What Kubernetes does

Kubernetes (K8s) runs containers across a group of machines. You declare the state you want ("five copies of this app, this much memory, reachable at this name") and controllers keep working to make reality match it: restarting failed containers, rescheduling work from failed nodes, rolling out updates. A **cluster** has a **control plane** (API server, the etcd database holding desired state, the scheduler, controllers; on EKS, AWS runs this for you across zones) and **nodes** (workers running a kubelet agent).

**Core objects.** **Pod:** the smallest unit, disposable, with its own IP. **Deployment:** keep N identical pods and roll out updates. **Service:** a stable name and virtual IP in front of changing pods. **Ingress** (or Gateway): HTTP routing into the cluster. **ConfigMap and Secret:** configuration kept out of images (Secrets are only base64-encoded, so encrypt and prefer an external secrets manager). **Namespace:** a partition for teams, quotas and access. **StatefulSet:** stable identity and storage. **DaemonSet:** one pod per node (log and monitoring agents). **PersistentVolumeClaim:** a request for durable storage, usually an EBS volume.

## 3.2 Requests, limits, probes and graceful shutdown

* **Request:** what the pod is guaranteed and what the scheduler uses to place it. **Limit:** the maximum it may use. Over a memory limit, the container is killed (OOMKilled, exit code 137). Over a CPU limit, it is *throttled*, which shows up as latency with no obvious CPU saturation.
* **Quality of service:** requests equal to limits is Guaranteed (evicted last); some requests is Burstable; none is BestEffort (evicted first). Set requests from measured use. Too high wastes money; too low causes crowding and evictions.
* **Placement:** taints and tolerations keep pods off special nodes; affinity and topology spread keep replicas apart (across zones). A **PodDisruptionBudget** limits how many copies can be taken down voluntarily; one that is too strict blocks node drains and upgrades.
* **Readiness probe:** "can this pod take traffic?" If it fails, the pod leaves the Service's endpoints but is not restarted. **Liveness probe:** "is it stuck?" If it fails, the container restarts; an aggressive one that depends on a downstream service can cause restart storms. **Startup probe:** gives slow starters time.
* **Graceful shutdown:** on deletion, the pod is removed from endpoints and sent a termination signal at about the same time, so traffic can still arrive briefly. Handle the signal, finish in-flight requests, add a short pre-stop delay, and allow enough termination grace time. This is the usual cause of errors that appear only during deploys.

## 3.3 StatefulSets: what they are, how they work, when to use them

**The problem they solve.** A Deployment treats pods as interchangeable: any pod can be killed and replaced by a new one with a new name, a new IP and an empty disk. That is right for stateless web services. Some software needs the opposite: each instance has an *identity* and its *own data*. A database replica must come back as "replica 2" with replica 2's data; a clustered system (a message broker, a search cluster) needs members that can find each other by stable names. A StatefulSet provides exactly that.

**What a StatefulSet guarantees.**

1. **Stable, predictable names.** Pods are named `name-0`, `name-1`, `name-2`, and a pod keeps its name when it is rescheduled.
2. **Stable network identity.** A StatefulSet requires a *headless Service* (a Service with `clusterIP: None`), which gives each pod its own DNS name such as `db-0.db.shop.svc.cluster.local`. Other pods, and the members themselves, can address a specific instance.
3. **Stable storage per pod.** A `volumeClaimTemplates` section creates a separate PersistentVolumeClaim for each pod (`data-db-0`, `data-db-1`). If pod `db-1` is rescheduled, it reattaches to the same claim and the same data.
4. **Ordered operations (by default).** Pods are created in order (0, then 1, then 2), each waiting for the previous to be ready, and removed in reverse order. This suits systems where the first member bootstraps the cluster. `podManagementPolicy: Parallel` removes the ordering when it is not needed.
5. **Controlled updates.** The rolling update goes from the highest ordinal down. A `partition` setting lets you update only pods with ordinal at or above a number: set it to 2 on a three-pod set and only `-2` updates, which gives you a canary. `OnDelete` updates a pod only when you delete it manually.

```yaml
apiVersion: v1
kind: Service
metadata: { name: db, namespace: shop }
spec:
  clusterIP: None                  # headless: DNS returns individual pod addresses
  selector: { app: db }
  ports: [{ port: 5432 }]
---
apiVersion: apps/v1
kind: StatefulSet
metadata: { name: db, namespace: shop }
spec:
  serviceName: db                  # the headless Service that provides pod DNS names
  replicas: 3
  selector: { matchLabels: { app: db } }
  updateStrategy:
    type: RollingUpdate
    rollingUpdate: { partition: 0 }
  template:
    metadata: { labels: { app: db } }
    spec:
      terminationGracePeriodSeconds: 60
      topologySpreadConstraints:
        - maxSkew: 1
          topologyKey: topology.kubernetes.io/zone
          whenUnsatisfiable: DoNotSchedule
          labelSelector: { matchLabels: { app: db } }
      containers:
        - name: db
          image: postgres:16
          ports: [{ containerPort: 5432 }]
          volumeMounts: [{ name: data, mountPath: /var/lib/postgresql/data }]
  volumeClaimTemplates:           # one PersistentVolumeClaim per pod
    - metadata: { name: data }
      spec:
        accessModes: ["ReadWriteOnce"]
        storageClassName: gp3
        resources: { requests: { storage: 100Gi } }
```

**When to use one.**

* Systems where each member has its own persistent state or identity: databases (as replicas), message brokers (Kafka, RabbitMQ), coordination services (ZooKeeper, etcd), search and analytics clusters (Elasticsearch, OpenSearch), caches with persistence (Redis clusters).
* Applications that need stable network names between members.

**When not to.** Stateless services (use a Deployment); data you can keep in a managed service (use RDS, ElastiCache or OpenSearch Service instead, because running a database on Kubernetes is real operational work); workloads that need one pod per node (DaemonSet).

**Important caveats.**

* **A StatefulSet alone does not make software highly available.** It gives identity and storage; replication, leader election, failover and backups are the application's job, so databases usually come with an **operator** that encodes that logic.
* **EBS volumes are zone-bound.** A pod's volume exists in one availability zone, so after a failure the pod must run in the same zone; if that zone has no capacity, the pod stays Pending. Spread replicas across zones, keep capacity per zone, and prefer replication at the application level.
* **"At most one" safety.** If a node becomes unreachable, Kubernetes will not start a replacement pod with the same identity until it is sure the old one is gone (to avoid two instances writing to the same data). So a pod on a failed node can stay stuck in `Terminating` until the node is confirmed down or removed; handle it with node lifecycle automation or careful manual intervention.
* **Volumes outlive the pods.** Scaling down or deleting a StatefulSet does *not* delete the claims by default (newer versions have a retention policy setting). Clean up deliberately, and know you pay for orphaned volumes.
* **Resizing and backups:** the StorageClass must allow volume expansion; take regular volume snapshots or application-level backups and test restores.
* **Disruption:** use a PodDisruptionBudget (for example allow one unavailable) so drains and upgrades do not remove quorum.
* **Updates:** use the partition setting for staged updates; for databases follow the vendor's upgrade procedure.

**Say it like this.** "A StatefulSet gives each pod a stable name, a stable DNS identity through a headless Service, and its own persistent volume, and it creates and updates pods in order. I use it when members have their own data and identity, I keep EBS's zone binding and the at-most-one behavior in mind, and wherever possible I choose a managed service instead."

---

## 3.4 Rapid-fire Kubernetes concepts

* **What happens on `kubectl apply` of a Deployment?** The request is authenticated and authorized, passes admission (mutating then validating), and is stored in etcd. The Deployment controller creates a ReplicaSet, which creates pods. The scheduler picks a node (filter nodes that fit, then score them), the kubelet pulls the image through the container runtime, the CNI sets up networking, and once readiness passes the pod joins the Service's endpoints.
* **How does the scheduler decide?** It filters by resources, taints, selectors, affinity and topology rules, then scores the rest; priority and preemption can evict lower-priority pods.
* **What does etcd do, and what matters on EKS?** It stores all cluster state. AWS manages it, so you watch object count and size (large Secrets and ConfigMaps hurt) and the API server's latency.
* **Controller versus operator?** A controller reconciles desired and actual state; an operator is a controller plus custom resource definitions that encode operational knowledge for an application.
* **Deployment, StatefulSet, DaemonSet, Job?** Stateless replicas with rolling updates; stable identity and storage with ordered updates; one pod per node; run to completion.
* **How does a rolling update work?** New pods are created within `maxSurge` and old ones removed within `maxUnavailable`, each step gated on readiness; `rollout undo` reverses it.
* **HPA formula?** Desired replicas equals the ceiling of current replicas times the current metric divided by the target metric, subject to minimum, maximum and stabilization.
* **HPA versus VPA?** HPA changes the number of pods, VPA changes requests; do not drive both from the same metric.
* **Taints and effects?** NoSchedule (do not place), PreferNoSchedule (try not to), NoExecute (also evict existing pods).
* **Eviction versus preemption versus OOM kill?** Eviction: the kubelet removes pods under node pressure; preemption: the scheduler removes lower-priority pods to place a higher-priority one; OOM kill: the kernel kills a process over its memory limit.
* **Do config changes reach running pods?** Mounted ConfigMap and Secret files update after a delay; environment variables do not, so a restart is needed.
* **EndpointSlices?** A scalable replacement for the Endpoints object listing a Service's ready pod addresses.
* **RBAC model?** Roles (namespaced) and ClusterRoles define verbs on resources; bindings attach them to users, groups or service accounts. Check with `kubectl auth can-i`.
* **Pod Security Standards?** Three levels: privileged, baseline, restricted; enforced per namespace by admission.
* **CNI, CSI and CRI?** The plugin interfaces for networking, storage and the container runtime.
* **kube-proxy modes?** iptables (default), IPVS (scales better), or replaced by an eBPF dataplane.
* **Version skew and upgrades?** Upgrade the control plane one minor version at a time; nodes may lag within the supported skew; removed APIs are the main break risk.
* **Native sidecars and init containers?** Init containers run to completion before the app starts; sidecars run alongside the app (newer versions manage their start order and shutdown natively).
* **Why PodDisruptionBudgets?** They protect availability during voluntary disruptions (drains, upgrades, consolidation); too strict a budget blocks maintenance.
* **Graceful termination sequence?** Pod marked terminating, removed from endpoints, pre-stop hook runs, termination signal sent, the app has the grace period to finish, then it is killed.

## 3.5 Kubernetes performance and security in brief (overview)

* **Performance:** CPU throttling (check throttled time), requests and limits, noisy neighbors (priority classes), slow node scale-out (headroom, small images), large clusters straining kube-proxy and the API server, cross-zone cost.
* **Security:** a role per workload (IRSA or Pod Identity) and block pod access to node credentials (IMDSv2, hop limit one); least-privilege RBAC and no standing cluster-admin; private or restricted API endpoint and audit logging; secrets encrypted with KMS and delivered from a secrets manager; admission policy (Kyverno or OPA Gatekeeper: no privileged pods, only signed images); default-deny network policy; image scanning and signing; patched node images; namespaces plus quotas, with separate clusters for sensitive workloads.

**Say it like this.** "I debug Kubernetes by layer: the pod's events and logs first, then scheduling and resources, then the Service and its endpoints, then DNS and network policy, then the AWS layer underneath: security groups, subnets, IAM and quotas."

# Part 4: Kubernetes networking, ingress, service discovery and service mesh

## 4.1 Kubernetes networking, end to end (and the AWS tie-in)

**The model.** Every pod has its own IP; pods reach each other without address translation. On EKS the default **VPC CNI** gives each pod a real VPC address from your subnets, so pod traffic is routed across the VPC like any instance (no overlay), VPC security groups, route tables and flow logs apply, and you must have enough free IPs. Each instance type limits pods per node (network cards times addresses); prefix delegation raises the limit, secondary address ranges avoid exhausting the main range, and IPv6 clusters remove the shortage.

**Services.** A ClusterIP is a virtual address: kube-proxy rules on every node (iptables by default, or IPVS or an eBPF dataplane) rewrite traffic sent to it so it reaches one ready pod. Types: ClusterIP (internal), NodePort, LoadBalancer (creates a cloud load balancer), ExternalName (DNS alias), and headless (no virtual IP; DNS returns pod addresses, used by StatefulSets). Service discovery and meshes are explained in 4.3.

**What happens on `curl http://my-svc:8080` from a pod.** (1) The pod asks CoreDNS, which returns the ClusterIP. (2) The pod connects to ClusterIP:8080. (3) The node's rules rewrite the destination to a ready pod IP (destination NAT) and record the connection in the tracking table. (4) The packet travels to that pod, directly across the VPC if it is on another node. (5) Replies are translated back through the tracking table. Failures can occur at each step: DNS, no ready endpoints, a network policy, a security group, or a full connection tracking table.

**Internet to a pod on EKS.** DNS resolves to the ALB created from an Ingress; the ALB ends TLS and, in **IP mode**, sends the request straight to a ready pod's VPC address (in instance mode it goes via node ports); security groups allow ALB to pod; the reply returns the same way. **externalTrafficPolicy: Local** keeps the client's source IP and avoids an extra hop, at the cost of uneven load.

**DNS.** CoreDNS answers cluster names (name.namespace.svc.cluster.local) and forwards the rest. Pods use search suffixes with ndots=5, so short names trigger several lookups, multiplying DNS load. Fixes: fully qualified names, tuned ndots, more CoreDNS replicas, a node-local DNS cache. Also watch the VPC resolver's packet limit.

**Network policies** are firewalls between pods. By default all traffic is allowed; once a policy selects a pod, only what is allowed passes. They need a CNI that enforces them (VPC CNI network policy support, Calico or Cilium). Classic mistake: a default-deny egress policy that forgets DNS.

**Debug order for "my Service is not reachable."** (1) Does the Service have endpoints (`kubectl get endpoints NAME`)? Empty means the selector does not match the pod labels or the pods are not ready. (2) Port versus targetPort. (3) From a debug pod (for example the netshoot image) test the pod IP, then the ClusterIP, then the name, to separate app, Service rules and DNS. (4) Network policies and security groups. (5) kube-proxy health. (6) Packet capture and connection tracking if intermittent.

## 4.2 Ingress, traffic management and DNS at scale

* **North-south path:** users, then CloudFront and WAF, then an ALB (IP mode) or NLB, then an ingress controller or the mesh gateway, then services. Gateway API is the newer, more expressive model for routing. The community ingress-nginx project was reported to be retiring in 2026, so check status before choosing it.
* **Per-tenant routing and limits.** Tenant-to-cell mapping happens outside the cluster (DNS or an edge lookup); rate limits at the edge (WAF rate rules) and at the gateway (Envoy rate limiting) protect shared capacity.
* **TLS.** ACM certificates on load balancers; cert-manager for in-cluster certificates and mesh roots; mutual TLS inside; monitor days to expiry and automate renewal.
* **DNS and service discovery.** CoreDNS inside the cluster; ExternalDNS creates Route 53 records from Ingress and Service objects; headless Services for stateful discovery; for multi-cluster, options include mesh multi-cluster, Route 53 private zones, or VPC Lattice.
* **Progressive delivery.** Argo Rollouts or Flagger shift traffic in steps (through weighted ALB target groups or mesh weights) and analyze metrics before continuing, rolling back automatically on failure.
* **Multi-region.** Route 53 latency or failover routing, or Global Accelerator for fast health-based steering without DNS caching; keep DNS TTLs in mind.
* **Locality.** Topology-aware routing (Kubernetes) or locality load balancing (Istio) keeps traffic in-zone when healthy, reducing latency and cross-zone cost.

## 4.3 Service discovery, service mesh and Istio

### 4.3.1 Service discovery: how does service A find service B?

**The problem.** In a container platform, instances of B come and go constantly: a deploy replaces every pod, an autoscaler adds three more, a node fails and its pods reappear elsewhere. Each new instance has a different IP address. If A had to know B's addresses, every change would break something. Service discovery is the mechanism that lets A say "I want B" and get a current, healthy answer.

**How Kubernetes does it (the default you rely on).**

1. **A stable name and virtual address.** You create a *Service* called `orders` in namespace `shop`. Kubernetes gives it a fixed virtual IP (the ClusterIP) and registers the DNS name `orders.shop.svc.cluster.local`. Neither changes when pods change.
2. **A live list of healthy backends.** Kubernetes watches the pods that match the Service's label selector and keeps a list of their addresses (stored as EndpointSlices). A pod is on the list only while it is *ready*: when its readiness probe fails, it is removed within seconds; when a new pod passes its probe, it is added.
3. **Name resolution.** When A's code looks up `orders`, the pod's DNS resolver asks CoreDNS, which returns the Service's ClusterIP (within the same namespace the short name works; across namespaces use `orders.shop`).
4. **Load balancing.** A connects to the ClusterIP; rules that kube-proxy maintains on each node (or an eBPF dataplane) pick one of the ready pod addresses. Section 4.1 walks through the packets.

**Variations to know.** A *headless* Service (no ClusterIP) makes DNS return the individual pod addresses, which stateful systems use to address a specific member (for example `db-0.db`). An *ExternalName* Service is a DNS alias to something outside the cluster. For cross-cluster or cross-environment calls, you need something more: an internal load balancer with a stable DNS name, a registry such as Consul or AWS Cloud Map, a mesh with multi-cluster support, or VPC Lattice.

**Client-side versus server-side discovery.** In *server-side* discovery (Kubernetes Services, a load balancer), the caller connects to one stable address and the platform picks a backend. In *client-side* discovery (Eureka with Ribbon, Consul with a smart client, gRPC client load balancing), the caller queries a registry, receives the list of instances, and chooses one itself. Client-side gives the caller more control (and avoids an extra hop) but puts discovery logic and failure handling into every client library, which is exactly what a mesh later takes out of the application.

**What goes wrong.** DNS caching in clients (a JVM caching an address forever, a client holding connections to dead pods), pods receiving traffic before they are ready (a missing or weak readiness probe), and long-lived connections that stick to old backends after a scale-out (HTTP/2 and gRPC). Good practice: correct readiness probes, short DNS caching in runtimes, connection lifetime limits or per-request balancing.

### 4.3.2 What a service mesh actually does, step by step

A service mesh adds a layer *on top of* discovery. Discovery answers "where is B?"; the mesh controls "how does A talk to B once we know?" (security, reliability, visibility). Walk through one call, A calling B, in sidecar mode:

1. **Interception.** Each pod has a proxy container (Envoy) beside the application. Rules in the pod's network namespace redirect all of the application's outgoing and incoming traffic through the proxy, so the application code does not change and does not know the proxy is there.
2. **Configuration.** A control plane (Istio's `istiod`) continuously pushes configuration to every proxy: the list of services and their healthy endpoints (taken from Kubernetes discovery), routing rules, timeouts, retry policy and security policy.
3. **Endpoint choice and resilience.** A's proxy picks a healthy B endpoint using a balancing algorithm (it balances per request, not per connection), applies the timeout, and retries on failure within the configured budget. If an endpoint keeps failing, outlier detection temporarily ejects it.
4. **Identity and encryption (mutual TLS).** The control plane acts as a certificate authority and gives each workload a short-lived certificate tied to its identity (typically the Kubernetes service account, in the SPIFFE format), rotated automatically. A's proxy and B's proxy perform a TLS handshake in which *both* present certificates, so each side knows exactly who the other is and the traffic is encrypted. The application sends plain HTTP to its local proxy.
5. **Authorization.** B's proxy checks policy: is the caller's identity allowed to call this service, method or path? Anything not allowed is rejected before it reaches the application. This is how you implement "only the checkout service may call payments."
6. **Telemetry.** Both proxies record request counts, errors and latency (the golden signals) for the A-to-B pair and can emit trace spans, with no application code.
7. **Traffic control.** The same rules enable canary releases ("send 5 percent of calls to version 2"), mirroring traffic for testing, fault injection, and locality-aware routing to prefer same-zone endpoints.

**When you need one, and when you do not.** The value grows with the number of services and teams: when you want encryption and identity everywhere without every team implementing TLS, when you need consistent retry and timeout behavior, when you want service-pair metrics for free, or when you need traffic splitting beyond what the load balancer offers. With a handful of services, Kubernetes Services plus good timeouts and network policies are often enough, and a mesh adds cost: extra CPU and memory per pod, slightly higher latency, a critical control plane, and harder debugging. The rest of this section covers Istio in particular, then Consul.

### 4.3.3 Istio specifics

**Architecture.** The control plane (**istiod**) distributes configuration and issues certificates. The data plane is **Envoy** proxies: in **sidecar mode**, one per pod; in **ambient mode**, a shared per-node component handles basic secure transport and optional per-namespace proxies handle HTTP features (fewer resources, newer, check maturity). **Ingress and egress gateways** manage traffic entering and leaving the mesh.

**The resources you should be able to name.**

* **Gateway and VirtualService:** how traffic enters and is routed (by host, path, header), with weights for canaries, retries, timeouts and fault injection.
* **DestinationRule:** load-balancing policy, connection pool limits, **outlier detection** (ejecting failing endpoints, a form of circuit breaking), and version subsets.
* **PeerAuthentication:** mutual TLS mode (permissive accepts both plain and encrypted; strict requires encryption).
* **AuthorizationPolicy:** which workload identities may call which services.
* **ServiceEntry:** describes external services; the **Sidecar** resource limits how much configuration each proxy loads (important for scale).

**Costs and risks.** Extra latency (usually small), CPU and memory per sidecar, the control plane becomes a critical dependency, upgrades are delicate (use revision-based canary upgrades), debugging is harder (an extra hop with its own errors), a bad configuration can break many services at once, retries can multiply load, long-lived connections (gRPC) do not rebalance by default, and app-versus-sidecar startup ordering can break early calls.

**Operating it.** `istioctl analyze` (configuration problems), `istioctl proxy-status` (is each proxy in sync), `istioctl proxy-config` (what a proxy actually has), proxy access logs with **response flags** (UF: upstream connection failure, UC: upstream connection terminated, UH: no healthy upstream, NR: no route, URX: retry limit hit), and metrics such as `istio_requests_total` and `istio_request_duration_milliseconds`. Migrate to strict mutual TLS namespace by namespace, from permissive to strict.

**When not to use one.** Few services, a small team, or a need only for encryption (a CNI with built-in encryption or a simpler tool may do). Alternatives: Linkerd, Cilium's mesh features, or AWS VPC Lattice. AWS announced the end of App Mesh support in 2026, so check before proposing it.

### 4.3.4 Istio in practice: configuration examples

**Turn on the mesh for a namespace.** Label the namespace so new pods get a sidecar (`istio-injection: enabled`, or a revision label when using revision-based upgrades), then restart the workloads so they are injected. Check with `istioctl proxy-status` that each proxy is in sync.

**Canary release with a traffic split.** A DestinationRule defines the versions (subsets by pod label); a VirtualService splits traffic by weight:

```yaml
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata: { name: orders, namespace: shop }
spec:
  host: orders
  subsets:
    - name: v1
      labels: { version: v1 }
    - name: v2
      labels: { version: v2 }
  trafficPolicy:
    connectionPool: { http: { http2MaxRequests: 1000, maxRequestsPerConnection: 100 } }
    outlierDetection: { consecutive5xxErrors: 5, interval: 10s, baseEjectionTime: 30s }   # eject failing endpoints
---
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata: { name: orders, namespace: shop }
spec:
  hosts: [orders]
  http:
    - route:
        - { destination: { host: orders, subset: v1 }, weight: 95 }
        - { destination: { host: orders, subset: v2 }, weight: 5 }     # the canary
      timeout: 3s
      retries: { attempts: 2, perTryTimeout: 1s, retryOn: "5xx,connect-failure" }
```

**Require encrypted traffic and restrict who may call.**

```yaml
apiVersion: security.istio.io/v1
kind: PeerAuthentication
metadata: { name: default, namespace: shop }
spec:
  mtls: { mode: STRICT }              # only mutual TLS traffic is accepted in this namespace
---
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata: { name: orders-callers, namespace: shop }
spec:
  selector: { matchLabels: { app: orders } }
  action: ALLOW
  rules:
    - from:
        - source: { principals: ["cluster.local/ns/shop/sa/checkout"] }   # only the checkout service identity
      to:
        - operation: { methods: ["GET", "POST"], paths: ["/orders*"] }
```

**Typical troubleshooting flow.** (1) `istioctl analyze` for configuration mistakes. (2) `istioctl proxy-status` to see whether proxies are in sync with the control plane. (3) `istioctl proxy-config routes|clusters|endpoints POD` to see what the proxy actually has. (4) Read the proxy's access log and its response flag (UF upstream connection failure, UC connection terminated, UH no healthy upstream, NR no route found, URX retry limit reached). (5) Check the metrics `istio_requests_total` and `istio_request_duration_milliseconds` by source, destination and response code. (6) For strict mutual TLS problems, check which side is not in the mesh. For certificate details, see 8.3.

### 4.3.5 Consul (HashiCorp): service registry and service mesh

**What it is.** Consul is a tool that provides **service discovery**, **health checking**, a **key-value store** and a **service mesh**. It is not Kubernetes-specific, which is its main reason to exist: it can give one view of services running on VMs, Kubernetes, ECS and other platforms.

**How it works.**

* **Servers and agents.** A small cluster of Consul **servers** (three or five, spread across zones) stores the service catalog and uses the **Raft** consensus protocol to agree on one consistent state, with a leader. If a majority of servers is lost, the cluster stops accepting writes (quorum loss), which is the key operational risk. Every machine that runs services also runs a lightweight **agent** (on Kubernetes, newer versions use a "dataplane" instead of per-node agents). Agents find each other and detect failures with a **gossip protocol** (Serf), which spreads membership and health information without a central poller.
* **Registration and health checks.** A service registers with its local agent (by configuration or API; on Kubernetes a sync component can copy Kubernetes Services into the catalog). The agent runs health checks (HTTP, TCP, gRPC, TTL heartbeat) and reports status. Unhealthy instances are removed from query results.
* **Lookup.** Clients find services through a **DNS interface** (for example `orders.service.consul` returns healthy addresses) or the HTTP API. Because Consul answers DNS itself, there is no client library requirement.
* **Key-value store.** For configuration and coordination (locks, leader election by applications).
* **Service mesh (Consul Connect).** Envoy sidecars give mutual TLS using certificates from Consul's built-in certificate authority (or Vault). **Intentions** are the authorization rules ("service A may call service B", at connection level or, with more configuration, at request level). **Mesh gateways** carry traffic between datacenters, Kubernetes clusters or administrative partitions without exposing every pod network, and cluster peering links independent clusters.
* **Access control.** ACL tokens control who can register services, read the catalog and change configuration; these must be bootstrapped and managed carefully.

**On Kubernetes and AWS.** A Helm chart installs Consul, syncs Kubernetes Services to and from the catalog, and injects sidecars with an annotation. The servers can run on EC2 or in the cluster, across three zones, with regular snapshots and tested restores. Plan upgrades carefully, because the servers are shared infrastructure.

**When it fits, and when it does not.** Consul fits a mixed estate (VMs, ECS and Kubernetes together), multi-datacenter or multi-cluster discovery with one set of policies, or an organization already standardized on HashiCorp tools. Inside a single Kubernetes cluster, native Services and DNS already do discovery, so Consul adds a system to run without much gain unless you want its cross-platform view or mesh. Compared with **Eureka** (an older, simple registry where instances register and renew leases, favoring availability over strict consistency), Consul is a stronger consistency, multi-purpose tool; compared with **Istio**, Consul's mesh spans non-Kubernetes workloads more naturally, while Istio has deeper Kubernetes-native traffic management. HashiCorp moved its products to a source-available license in 2023, so check licensing and any fork before adopting.

# Part 5: EKS architecture and platform design

## 5.1 EKS architecture in depth

* **Control plane (managed).** AWS runs the API servers and etcd across multiple zones; you cannot touch etcd or the scheduler's settings, but you can enable control plane logs (API, audit, authenticator, scheduler, controller manager) to CloudWatch. The API endpoint can be public, private, or both, with an allowed-address list. AWS places network interfaces in your subnets so the control plane can reach nodes and webhooks, which is why security groups and subnets matter for webhooks. The API server throttles clients under load (API priority and fairness), so runaway controllers cause slow `kubectl` and failed deploys.
* **Data plane choices.** *Managed node groups* (AWS handles image updates and draining), *Karpenter-managed nodes* (just-in-time, flexible), *Fargate* (a micro-VM per pod: no node management, but no DaemonSets, limited features, higher per-pod cost), *self-managed nodes*, and EKS Auto Mode (AWS-managed compute; check current maturity). Run critical add-ons (CoreDNS, the controller that runs Karpenter) on a stable managed node group, not on nodes Karpenter may replace.
* **Add-ons you must manage and upgrade in order:** VPC CNI, kube-proxy, CoreDNS, EBS and EFS CSI drivers, AWS Load Balancer Controller, metrics-server, ExternalDNS, cert-manager, the autoscaler. Treat each as versioned software with a compatibility matrix.
* **Networking details.** The VPC CNI assigns pod IPs from node network cards. Its warm-pool settings (warm IP, minimum IP, warm ENI targets) decide how many addresses each node holds in reserve: too high wastes your address space, too low slows pod startup. Prefix delegation, custom networking (pods in a secondary range), security groups for pods, and IPv6 are the scaling and isolation tools.
* **Identity.** IAM roles for service accounts (IRSA) or EKS Pod Identity for pods; EKS access entries for people and automation, mapped to Kubernetes RBAC.
* **Storage.** EBS (one pod at a time, zone-bound), EFS (shared, NFS; mount targets need security groups allowing port 2049), snapshots through the CSI snapshot support.
* **Practical limits to reason about.** Pods per node (network cards and addresses), nodes and objects per cluster before the API server strains, Service count (iptables rule updates), and cluster-wide IP space. When you approach limits, the answer is usually more clusters (a smaller blast radius), not a bigger one.

## 5.2 EKS specifics

* **Nodes not joining:** the node role must be authorized (EKS access entry or the older aws-auth map) with the standard node policies; it needs a network path to the cluster API; bootstrap settings must be right. `journalctl -u kubelet` on the node shows the error.
* **`kubectl` unauthorized:** refresh with `aws eks update-kubeconfig`, confirm the identity with `aws sts get-caller-identity`, check the identity has an access entry, and be on the VPC network if the endpoint is private.
* **Pod permissions (IRSA or Pod Identity):** with IRSA, the service account needs the role annotation, the cluster's OIDC provider must be registered in IAM, and the role's trust policy must name the right provider, namespace and service account. From inside the pod, `aws sts get-caller-identity` shows which identity it really has (the node's role means injection failed).
* **Load balancer stuck pending:** the AWS Load Balancer Controller must be installed with its IAM role, subnets need the discovery tags, and there must be free IPs. Describe the Service or Ingress for events.
* **PVC pending:** the EBS CSI driver and its role, a StorageClass, the wait-for-first-consumer binding mode (EBS is zone-bound), and capacity.
* **Autoscaling:** the HPA needs the metrics server and CPU requests on pods. **Karpenter** launches nodes just in time for pending pods and consolidates idle nodes; if it does not scale, check node pool limits, requirement mismatches, subnet and security group discovery tags, vCPU quotas and instance availability.
* **Upgrades:** one minor version at a time. Scan for removed APIs first, upgrade the control plane, then nodes (new nodes, drain old, respecting PDBs), then add-ons (CNI, CoreDNS, kube-proxy). Roll cell by cell, canary first.

## 5.3 The design decisions an architect must defend

**Cluster boundaries (the biggest decision).**

| Option | Strengths | Weaknesses | Fits |
| :--- | :--- | :--- | :--- |
| One cluster per cell | Smallest blast radius, matches cell design, independent upgrades | Many clusters to operate; needs strong automation; some idle capacity | Cell-based identity platform |
| Shared cluster per region | Cheaper, simpler, better bin-packing | One upgrade or API server problem hits everyone; tenant coupling | Dev, staging, internal tools |
| Cluster per environment or team | Clear ownership | Sprawl; uneven standards | Small organizations |

**Multi-AZ.** Spread nodes and replicas across at least three zones with topology spread constraints; keep enough headroom that losing a zone does not overload the others (run below about two-thirds utilization); for zone-bound storage, plan per-zone capacity; use topology-aware routing to cut cross-zone traffic and latency.

**Multi-region patterns.**

* **Active-passive (warm standby):** a second region holds a ready cluster rebuilt from Terraform and GitOps, data replicated, minimal traffic until failover. Simpler, slower failover.
* **Active-active:** each region serves live traffic. Feasible only if the data layer allows it; with a single-writer database per cell, a cell is homed in one region, so regions serve different cells while each cell has a standby elsewhere.
* **Clusters as cattle:** any cluster can be recreated from code (Terraform for the cluster, GitOps for everything inside), with state kept outside (databases, object storage, secrets manager). Back up what Git does not hold (volumes, custom resources created at runtime) with a tool such as Velero.

**Multi-tenancy models.** Namespace per team (cheap, soft isolation: quotas, limit ranges, RBAC, network policies, pod security standards, priority classes); dedicated node pools per tenant (taints and tolerations, protects against noisy neighbors and some attacks); dedicated cluster (hard isolation, for sensitive or regulated tenants). Choose by trust level, compliance and cost, and add cost allocation by labels.

**Upgrade strategy.**

| | In-place | Blue/green clusters |
| :--- | :--- | :--- |
| How | Upgrade the control plane, then replace nodes, then add-ons | Build a new cluster at the new version, shift traffic, retire the old one |
| Rollback | Hard (control plane cannot be downgraded) | Easy (shift traffic back) |
| Cost and effort | Lower | Higher, needs traffic shifting and external state |

A common policy: in-place for most, canary clusters first, a maximum version lag (for example never more than one minor behind), automated deprecated-API scans, and blue/green for the riskiest upgrades.

**Fleet management.** Terraform defines clusters; ArgoCD ApplicationSets (or a similar tool) apply the same platform add-ons and policies to every cluster; an inventory records each cluster's version and add-on versions; upgrades roll in waves with health checks, like cells.

### 5.3.1 Operating a fleet of about 100 clusters (a cell-based platform)

Running one cluster well is a Kubernetes problem; running a hundred is a **fleet-management** problem. The goal is that a hundred clusters behave like one: same baseline, same upgrade process, same alerts, so a human never has to treat a cluster as special.

**Lifecycle, end to end.**

1. **Create:** a cluster is created from a manifest (cell name, region, size, version) through Terraform. The same run creates the network, the EKS cluster, node capacity, IAM roles and the connection to the GitOps controller. This is the data-driven cell pattern from Part 2: owners write a few values, modules supply the standards.
2. **Bootstrap:** the GitOps controller (for example Argo CD running in the cluster) starts reading the fleet repository and installs the platform add-ons (CNI settings, CoreDNS tuning, ingress, secrets operators, autoscalers, policy engine, observability agents) in a defined order.
3. **Configure per cluster:** a small set of variables (cluster name, region, cell, environment) flows into the add-on configuration so one set of manifests serves every cluster.
4. **Operate:** the fleet is watched centrally (is every cluster reconciled, on the right versions, reporting metrics?).
5. **Upgrade and patch:** in waves (see 12.5).
6. **Retire:** drain traffic, remove from the inventory, destroy through Terraform.

**Keeping clusters consistent.**

* **One source of truth:** a *fleet repository* with a shared base and per-ring or per-cluster overlays. Changes are pull requests; clusters pull them. Manual changes are reverted by self-healing or flagged as drift.
* **Rings (waves):** group clusters into rings (canary, early, broad, critical). A change merges first to the canary ring's path or branch and is promoted after health gates pass. This is how a bad platform change (a policy, an add-on version) hits a handful of clusters instead of all hundred.
* **Inventory and reporting:** a table of cluster, version, add-on versions, last reconcile time, and owner. A cluster that stops reconciling, or falls more than one version behind, raises an alert.
* **Version policy:** at most one minor Kubernetes version behind, add-ons within the supported range, and a standing upgrade cadence so upgrades are routine.
* **Standard add-on bundle:** pinned versions, tested together before release (the "platform release"), so you never combine untested versions in production.

**What gets harder with scale.** Every manual step multiplies by the number of clusters; configuration drift appears wherever a hand edit was allowed; shared dependencies (container registry, Git server, secrets manager, observability backend) become fleet-wide single points of failure; AWS account quotas (vCPUs, network interfaces, load balancers, API rates) are consumed by all clusters together; and costs add up from small per-cluster fixed charges (control plane fee, NAT gateways, monitoring agents). Mitigations: automate everything, keep the dependencies highly available and cached near the clusters, track quotas per account, and review the fixed cost of a cluster, because it decides how many cells are affordable.

**Say it like this.** "At a hundred clusters, the unit I manage is the fleet, not the cluster. Clusters come from a manifest, are configured by GitOps from one repository, change in rings with health gates, and are tracked in an inventory that alerts on drift, version lag and silence."

## 5.4 Taking a new containerized service to production on EKS (end to end)

**The scenario.** A team has a service packaged as a Docker image and wants to run it on EKS in production as a new service on your platform. What must you think through? This section is the full checklist, with the reasoning behind each item, in the order you would do the work. (Migrating an *existing* service from another runtime, such as ECS, adds a few steps; see 12.4.)

### 5.4.1 What must exist on the platform first

A new service should not be the thing that forces you to build the platform. Before onboarding, confirm that the platform provides:

* **A cluster and network that fit:** subnets with enough free IPs for the expected pod count, nodes across three zones, and capacity (managed node groups or Karpenter) with headroom.
* **Standard add-ons running and monitored:** the CNI, CoreDNS, the load balancer controller, storage drivers, metrics-server, ExternalDNS, cert-manager and an external secrets operator. If one of these is broken, every service is affected.
* **Identity and namespaces:** SSO-based access, a namespace for the team created from a template (quota, limit range, default-deny network policy, RBAC, pod security level, cost labels).
* **A delivery path:** CI that builds and scans the image, and a deployment mechanism (GitOps with Argo CD or Spinnaker) with the ability to roll back.
* **Observability pipelines:** logs, metrics and traces collection already working, so the new service only needs to emit data.
* **Guardrails:** admission policy (in enforcement for the basics) so that unsafe configurations are rejected rather than reviewed by hand.

### 5.4.2 Make the container production-ready

Kubernetes will run almost any image, but production needs behavior that a container run by hand does not show.

* **Run as a non-root user,** with a minimal base image and no build tools in the final image. A smaller image pulls faster and has fewer vulnerabilities.
* **Log to standard output and standard error** (structured JSON if possible). Kubernetes and the log agent collect from there; writing to files inside the container fills the node's disk and loses the logs when the pod dies.
* **Read configuration from the environment or mounted files,** not baked into the image, so the same image runs in every environment.
* **Expose health endpoints with distinct meanings.** *Readiness* means "I can serve traffic right now" (dependencies reachable, caches warm) and may go false temporarily; *liveness* means "I am stuck and need a restart" and should be cheap and independent of downstream services (a liveness probe that calls the database will restart every pod when the database blips, turning a small problem into an outage); a *startup* probe gives slow starters time before liveness begins.
* **Shut down gracefully.** On termination the pod receives a SIGTERM and the platform simultaneously removes it from load balancing. The application should stop accepting new work, finish in-flight requests and exit within the grace period. A short pre-stop delay (a few seconds) covers the lag between "removed from endpoints" and "load balancers stop sending".
* **Be a good network citizen:** set timeouts on every outbound call, retry only safe operations with backoff and jitter, reuse connections, and handle DNS changes (do not cache addresses forever).
* **Be stateless,** or make the state explicit: sessions in a shared store, files in object storage, databases outside the pod. A pod can be killed and rescheduled at any time.
* **Pin the image** by version tag (better, by digest) from your registry, and scan it.

### 5.4.3 Describe the service to Kubernetes

The main objects, and why each exists:

* **Deployment:** keeps N copies running and rolls out new versions gradually.
* **Service:** the stable name and address (discovery, see 4.3.1).
* **Ingress or Gateway route:** exposes it to outside traffic if it is public.
* **ServiceAccount:** the identity the pod uses, linked to an IAM role.
* **ConfigMap and external secret:** configuration and credentials.
* **HorizontalPodAutoscaler:** adjusts replicas to load.
* **PodDisruptionBudget:** limits how many replicas may be taken down at once by maintenance.
* **NetworkPolicy:** the pod's allowed network connections.

A Deployment with the production basics (resources, probes, spread across zones, a restricted security context, graceful shutdown):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: orders
  namespace: shop
spec:
  replicas: 3
  strategy:
    rollingUpdate: { maxSurge: 25%, maxUnavailable: 0 }   # never drop below desired capacity during a rollout
  selector:
    matchLabels: { app: orders }
  template:
    metadata:
      labels: { app: orders }
    spec:
      serviceAccountName: orders          # linked to an IAM role (IRSA or Pod Identity)
      terminationGracePeriodSeconds: 45
      topologySpreadConstraints:          # keep replicas in different zones
        - maxSkew: 1
          topologyKey: topology.kubernetes.io/zone
          whenUnsatisfiable: ScheduleAnyway
          labelSelector: { matchLabels: { app: orders } }
      securityContext:
        runAsNonRoot: true
        seccompProfile: { type: RuntimeDefault }
      containers:
        - name: orders
          image: 111122223333.dkr.ecr.us-east-1.amazonaws.com/orders@sha256:EXAMPLEDIGEST   # pinned by digest
          ports: [{ containerPort: 8080 }]
          resources:
            requests: { cpu: 500m, memory: 512Mi }   # from measured usage; drives scheduling and autoscaling
            limits: { memory: 512Mi }                # memory limit; set a CPU limit only deliberately
          readinessProbe: { httpGet: { path: /ready, port: 8080 }, periodSeconds: 5, failureThreshold: 3 }
          livenessProbe:  { httpGet: { path: /healthz, port: 8080 }, periodSeconds: 10, failureThreshold: 3 }
          startupProbe:   { httpGet: { path: /healthz, port: 8080 }, periodSeconds: 2, failureThreshold: 30 }
          lifecycle:
            preStop: { exec: { command: ["sleep", "10"] } }   # let load balancers drain first
          securityContext:
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
            capabilities: { drop: ["ALL"] }
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata: { name: orders, namespace: shop }
spec:
  minAvailable: 2
  selector: { matchLabels: { app: orders } }
```

**Sizing requests and limits.** Requests are what the scheduler reserves and what the autoscaler measures against, so set them from observed usage (a load test or the previous runtime's metrics), with some headroom. Too low and pods are crowded together and evicted under pressure; too high and you pay for idle capacity. A memory limit protects the node (the pod is killed if it exceeds it); CPU limits throttle, which can add latency to bursty services, so many teams set CPU requests and leave CPU limits off or generous, after measuring.

**Replicas and disruption.** At least three replicas across three zones for a production service, so one zone loss or one node drain does not take it down. The PodDisruptionBudget tells maintenance operations (node drains, Karpenter consolidation, upgrades) to keep at least two available; do not set it so strictly that nothing can ever be drained.

### 5.4.4 Access control (who and what may do what)

Think of three separate identities.

1. **People.** Engineers reach the cluster through SSO mapped to EKS access entries, and then to Kubernetes RBAC roles scoped to namespaces: developers can deploy and view their own namespace; only the platform team can change cluster-wide objects; production changes go through the pipeline, not direct `kubectl`. A break-glass role exists for emergencies and triggers an audit alert when used.
2. **Automation.** The CI/CD system uses short-lived credentials obtained through OIDC (no long-lived access keys stored in the pipeline), with a role that can deploy only to its own namespaces and push only to its own repositories.
3. **The workload itself.** The pod needs AWS permissions (read a bucket, call a queue). Create an IAM role with only those permissions and link it to the service account (IRSA or EKS Pod Identity), so credentials are issued to that pod alone, short-lived and tied to its identity. Do not let pods use the node's role (it would give every pod on the node the same permissions), and block access to the instance metadata credentials (IMDSv2 with a hop limit of one).

Inside Kubernetes, give the service account no extra RBAC permissions unless the application really uses the Kubernetes API, and disable automatic mounting of the API token when it does not.

### 5.4.5 Ingress: traffic coming in

Decide first whether the service is **public** (called from the internet), **internal** (called by other services or corporate users), or **cluster-only**.

* **Cluster-only:** a ClusterIP Service is enough.
* **Internal:** an internal load balancer (ALB or NLB in private subnets) through an Ingress or Service annotation, with security groups limiting callers.
* **Public:** the standard path is users, then DNS, then CloudFront and WAF (rate limits, bot rules, managed rule sets), then an ALB created from an Ingress by the AWS Load Balancer Controller, then the pods. Use **IP target mode** so the load balancer sends traffic directly to pod addresses (no extra node hop).
* **TLS:** terminate at the ALB with an ACM certificate (renewed automatically), and re-encrypt to the pod or use the mesh for encryption inside the cluster if the requirements demand it. Monitor days to expiry.
* **DNS:** ExternalDNS creates the Route 53 record from the Ingress, so the record is part of the same change.
* **Health checks and draining:** the load balancer health check path and thresholds must match the readiness endpoint, and the deregistration delay should be longer than the application's shutdown time.
* **Protection:** WAF rate rules per client, request size limits, and (for authenticated APIs) token validation at the gateway or mesh.

### 5.4.6 Egress: traffic going out

Pods usually need to reach databases, other AWS services, and sometimes the internet.

* **Private AWS services:** use VPC endpoints (S3 and DynamoDB as gateway endpoints; ECR, STS, Secrets Manager and others as interface endpoints) so traffic stays on the AWS network and does not consume NAT capacity or cost.
* **Databases:** allow the connection with a security group (the database's group accepts the application's group on the database port) and, in Kubernetes, with an egress network policy to the database subnet. Use security groups for pods if the database trusts only a specific group.
* **The internet:** pods in private subnets reach it through NAT gateways (one per zone). If a partner requires fixed source addresses, those are the NAT gateways' Elastic IPs; for many connections to one destination, watch NAT port exhaustion.
* **Control it:** by default a pod can call anything, so add default-deny egress with explicit allows (do not forget DNS), and for high-assurance environments route outbound traffic through a filtering proxy or firewall that allows only approved domains. Log egress for investigation.

A starter network policy for the service (allow traffic only from the ingress namespace, allow DNS, allow the database subnet):

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata: { name: orders, namespace: shop }
spec:
  podSelector: { matchLabels: { app: orders } }
  policyTypes: [Ingress, Egress]
  ingress:
    - from:
        - namespaceSelector: { matchLabels: { kubernetes.io/metadata.name: ingress } }
      ports: [{ port: 8080 }]
  egress:
    - to:
        - namespaceSelector: { matchLabels: { kubernetes.io/metadata.name: kube-system } }
          podSelector: { matchLabels: { k8s-app: kube-dns } }
      ports: [{ port: 53, protocol: UDP }, { port: 53, protocol: TCP }]
    - to: [{ ipBlock: { cidr: 10.0.32.0/20 } }]      # the database subnets
      ports: [{ port: 3306 }]
```

### 5.4.7 Service-to-service communication

* **Discovery:** call other services by their Kubernetes Service name (see 4.3.1). Keep the call graph documented, so you know who depends on whom.
* **Allowing the call:** with network policies, the callee must allow the caller's namespace or labels, and the caller's egress must allow the callee. With a mesh, an authorization policy names which identities may call the service.
* **Encryption and identity:** if internal traffic must be encrypted and authenticated (usual in regulated environments), either the application handles TLS (and certificate rotation) in every service, or a mesh provides mutual TLS automatically (see 4.3.2). Decide per environment, because partial adoption leaves gaps.
* **Reliability between services:** timeouts shorter than the caller's own timeout, retries with backoff and jitter on safe operations only, circuit breaking and connection limits so a slow dependency cannot exhaust the caller, and a defined behavior when the dependency is down (degrade, queue, or fail fast).
* **Asynchronous options:** queues or streams between services decouple availability and absorb bursts; they trade immediacy for resilience.
* **Versioning:** keep APIs backward compatible so that during a rollout old and new versions can coexist.

### 5.4.8 Security hardening

* **Pod level:** restricted pod security (non-root, no privilege escalation, dropped capabilities, read-only root filesystem, default seccomp profile). The Deployment above shows the settings; admission policy enforces them.
* **Supply chain:** the image is built in CI, scanned for vulnerabilities, signed, and stored in a private registry; admission verifies the signature and the registry. Pin by digest.
* **Secrets:** stored in a secrets manager and delivered by an external secrets operator (or a CSI driver), encrypted at rest with KMS; never in the image, the Git repository or plain environment definitions. Plan rotation: pods must pick up a new value (a reloader that restarts them, or applications that re-read the file), and credentials should support two valid values during a rotation window.
* **Network:** default-deny policies, security groups for pods where needed, WAF at the edge, and encryption in transit.
* **Data:** encryption at rest for volumes and databases, with key policies.
* **Detection:** audit logs, runtime threat detection (GuardDuty EKS or Falco), alerts on anomalies such as a shell opened in a production pod.
* **Compliance:** record who deployed what and when (the pipeline and Git history provide it), patch SLAs, and a documented review.

### 5.4.9 Observability

Make the service observable before it takes traffic.

* **Metrics:** expose application metrics (request rate, errors, latency histograms, saturation); a ServiceMonitor tells Prometheus to scrape them. Platform metrics (restarts, throttling, memory, replicas) arrive from kube-state-metrics and the kubelet.
* **Logs:** structured, with a request or trace ID, no secrets; collected by the node agent with Kubernetes metadata (namespace, pod, version).
* **Traces:** OpenTelemetry instrumentation, or mesh-generated spans, with trace IDs in the logs.
* **SLOs and alerts:** define the SLIs that reflect user experience (success rate, latency), set an SLO, and alert on burn rate (page on fast burn, ticket on slow burn). Every alert has an owner and a runbook.
* **Dashboards:** one per service from the standard template (golden signals plus dependencies and deploy markers).
* **Synthetic checks:** a probe that exercises the real user path from outside.
* **Cost:** labels so spend is attributed to the team and service.

### 5.4.10 Scaling and resilience

* **Pods:** an HPA based on a metric that reflects load (requests per second per pod, or queue depth), not only CPU, with a sensible minimum (at least the zone count) and maximum, and a stabilization window to avoid flapping.
* **Nodes:** Karpenter or the autoscaler adds capacity when pods are pending; node startup takes time, so keep headroom (placeholder pods) for spiky services.
* **Dependencies:** know the downstream limits (database connections, third-party rate limits) and cap concurrency so scaling the service does not overwhelm them.
* **Failure behavior:** what happens if a zone, a node, or a dependency fails? Test it: kill pods, drain a node, block a dependency, and watch the metrics.
* **Load test:** run a realistic test on the target configuration, including a scale-out and a zone loss, and record capacity per pod.

### 5.4.11 Delivery and release

* **Pipeline:** build once, test, scan, sign, push; deploy the same image digest through the environments.
* **Release strategy:** rolling updates are the default; for risky services use canary or blue/green with automated analysis (Argo Rollouts, or Spinnaker's canary analysis) and automatic rollback on SLO burn.
* **Configuration through Git:** the manifests (or Helm values) live in a repository; changes are reviewed; GitOps applies them (see 7.3).
* **Rollback:** know the exact action (revert the commit, or roll back the release), and rehearse it.

### 5.4.12 Production readiness review (the gate to go live)

| Area | Question | Done |
| :--- | :--- | :--- |
| Ownership | Named owner, on-call rotation, escalation path | [ ] |
| Reliability | At least three replicas across zones, PDB, probes, graceful shutdown, tested failure behavior | [ ] |
| Capacity | Requests and limits from measurement, autoscaling configured, load test results | [ ] |
| Security | Restricted pod settings, signed image, least-privilege IAM role, secrets from a manager, network policies, WAF rules | [ ] |
| Network | Ingress and egress defined, DNS and TLS automated, dependencies and allow-lists documented | [ ] |
| Observability | Metrics, logs, traces, SLO and burn-rate alerts, dashboard, runbooks | [ ] |
| Delivery | Pipeline, rollback rehearsed, release strategy chosen | [ ] |
| Data | Backups, retention, encryption, migration plan | [ ] |
| Cost | Labels, a budget, right-sizing reviewed | [ ] |
| Compliance | Required reviews and evidence recorded | [ ] |

**Go-live and the first weeks.** Start with a small share of real traffic or a limited audience, watch the SLO metrics and the saturation signals, increase in steps, and keep a clear rollback. After launch, review the first incidents and the cost, tune requests and autoscaling, and feed lessons back into the service template so the next service starts with them.

**Say it like this.** "I make the container production-ready first, then describe it to Kubernetes with probes, resources, spread and disruption budgets. I give people, automation and the workload separate least-privilege identities, define ingress and egress explicitly, secure the supply chain and secrets, and make it observable with SLO alerts before it takes traffic. Then I load test it, release it gradually with an automatic rollback, and gate go-live on a readiness review."

## 5.5 Common Kubernetes problems at large scale, and how to avoid them

At small scale Kubernetes mostly fails because of mistakes in one workload. At large scale, the failures come from two sources: **shared limits** that everything depends on (the API server, IP addresses, DNS, the registry, the network dataplane), and **change** (upgrades, policies, autoscaling) that touches many things at once. Each problem below says what happens, why, how to notice it, and how to avoid or reduce it. (Single-workload symptoms are in 10.1 and Part 10.)

**1. The API server becomes a bottleneck.** *What you see:* `kubectl` is slow, deployments time out, controllers report errors or 429 (too many requests), and cluster behavior lags. *Why:* thousands of nodes and objects, controllers and scripts that list everything repeatedly instead of watching, very large objects (big ConfigMaps and Secrets, Helm release records), and slow admission webhooks that sit in the path of every write. *Notice:* API request latency and rejection metrics, audit logs showing the heaviest clients. *Avoid:* write controllers with informers and caches, set client rate limits, keep objects small, give webhooks tight timeouts and high availability, and, most importantly, split into more clusters (or cells) before you approach the limits rather than after.

**2. Running out of IP addresses.** *What you see:* pods stay pending or fail to start with network errors, nodes cannot add pods, while CPU and memory look fine. *Why:* on EKS each pod uses a VPC address, subnets were sized for instances not pods, each node holds spare addresses in reserve, and each instance type limits pods. *Notice:* free addresses per subnet, pending pods with CNI errors. *Avoid:* plan address ranges for the final scale, use prefix delegation, a secondary range for pods, or an IPv6 cluster, tune the CNI's warm-address settings, and monitor free addresses.

**3. DNS overload.** *What you see:* intermittent failures and slow requests that look random, errors resolving names, sometimes only for pods on certain nodes. *Why:* CoreDNS too small for the cluster, the ndots setting multiplying lookups (a name with fewer than five dots tries several suffixes first), a high volume of lookups from chatty applications, and AWS's limit of about 1,024 packets per second per network interface to the VPC resolver (CoreDNS pods concentrated on a few nodes hit it). *Notice:* CoreDNS latency and SERVFAIL rates, resolver drops. *Avoid:* scale CoreDNS with the cluster, run a node-local DNS cache, use fully qualified names or lower ndots, spread DNS pods across nodes, and cache sensibly in the application.

**4. Network dataplane limits.** *What you see:* connection resets, timeouts under load, slow rule updates. *Why:* connection tracking tables fill (the kernel starts dropping packets), ephemeral ports run out with many short connections, NAT gateways hit per-destination connection limits, and kube-proxy in iptables mode slows down when there are thousands of Services because every change rewrites large rule sets. *Notice:* kernel messages about a full tracking table, NAT port allocation errors, node packet-drop counters. *Avoid:* reuse connections (keep-alive, pools), raise tracking limits where appropriate, add NAT capacity or endpoints, switch to IPVS or an eBPF dataplane, and keep the number of Services per cluster reasonable.

**5. Node churn from autoscaling and interruptions.** *What you see:* intermittent errors during scale-in, constant pod restarts, nodes appearing and disappearing, deployments that never settle. *Why:* aggressive consolidation, spot interruptions, nodes expiring on schedule, pods with one replica or no disruption budget, and applications that do not shut down gracefully. *Avoid:* multiple replicas spread across zones, PodDisruptionBudgets that allow maintenance but protect availability, graceful shutdown with a pre-stop delay, disruption budgets in the autoscaler (a cap on how many nodes it may replace at once), and on-demand capacity for critical services.

**6. Resource contention and wrong sizing.** *What you see:* noisy neighbors, latency spikes with low average CPU, out-of-memory kills, evictions, bills much higher than expected. *Why:* requests missing or guessed, CPU limits throttling bursty services, no quotas so one team consumes the cluster, and over-requested resources leaving nodes idle. *Notice:* throttled-period ratio, working-set memory versus limit, requested-versus-used efficiency. *Avoid:* requests from measurement (VPA recommendations help), deliberate CPU limits, namespace quotas and limit ranges, priority classes, separate node pools for batch work, and regular right-sizing reviews.

**7. Upgrades and version drift.** *What you see:* an upgrade breaks workloads, clusters on many different versions, add-ons incompatible with the cluster version, drains that never finish. *Why:* removed APIs, add-on version mismatches, strict PDBs, manual and infrequent upgrades that accumulate risk, and no inventory of what runs where. *Avoid:* a version policy (no more than one minor behind), automated deprecated-API scans, canary clusters and waves, add-ons upgraded in order, blue/green clusters for the riskiest upgrades, and treating upgrades as routine engineering work with a schedule (strategy in 5.3).

**8. Policy and admission outages.** *What you see:* no deployment can be created anywhere, pods fail to start with webhook errors. *Why:* a new strict policy, or an admission webhook that is down while configured to fail closed, so every create or update is rejected. A single platform change affects every team at once. *Avoid:* roll out policies in audit mode first and then enforce gradually by namespace, make webhooks highly available with short timeouts, use fail-open for non-critical checks, exclude critical system namespaces, test policies in a canary cluster, and keep a documented break-glass step.

**9. Image pulls and registry limits.** *What you see:* slow scale-out, pods stuck pulling images, rate-limit errors, an outage when the registry is unreachable. *Why:* many nodes pulling large images simultaneously, public registry limits, a registry in one region becoming a dependency of every cluster. *Avoid:* small images, a private registry with replication or a pull-through cache near the clusters, pre-pulled or cached images in the node image for critical components, VPC endpoints for the registry, and staged scale-out.

**10. Observability that cannot keep up.** *What you see:* the metrics system runs out of memory, dashboards are slow, the monitoring bill explodes, alerts are ignored. *Why:* high cardinality (pod names, request IDs as labels), too many metrics from every pod, unbounded log volume, and alerts on causes instead of symptoms. *Avoid:* aggregate by workload, drop unneeded labels, set per-team limits, sample traces, control log volume at ingestion, alert on SLO burn, and run the monitoring platform outside the failure domain of the clusters it watches.

**11. Configuration drift between clusters.** *What you see:* clusters that behave differently, fixes that work in one and not another, unreviewed manual changes. *Why:* hand edits during incidents, per-cluster special cases, and no single source of truth. *Avoid:* GitOps with self-healing, a shared base with small overlays, policy as code, an inventory of versions and settings, and restricted write access to production.

**12. Secrets and certificate expiry.** *What you see:* sudden outages at a round-number date, authentication failures after a rotation. *Why:* manual certificate renewal, rotation that pods do not pick up, and no expiry monitoring. *Avoid:* automated issuance and renewal (cert-manager, ACM), alerts weeks before expiry, a reloader or rolling restart on rotation, two valid credentials during a rotation window, and regular rotation drills.

**13. Stateful workloads.** *What you see:* pods stuck because a volume is attached to another node or exists in another zone, slow recovery after failures, data loss fears. *Why:* block volumes are zone-bound and attach to one node, failover is more complex than for stateless services. *Avoid:* prefer managed databases and object storage, if you must run state use StatefulSets with per-zone capacity, tested backups and restores, and anti-affinity.

**14. Cost overruns.** *What you see:* spend grows faster than traffic. *Why:* over-requested resources, idle nodes, spot and on-demand imbalance, cross-zone traffic, NAT and logging costs, many small clusters. *Avoid:* right-sizing, autoscaler limits and consolidation, topology-aware routing, VPC endpoints, log and metric controls, cost allocation by label with a cost tool (OpenCost or similar), and regular reviews.

**15. Retry storms and cascading failures.** *What you see:* a small slowdown becomes a full outage, load keeps climbing even though users did not increase. *Why:* missing timeouts, aggressive retries, shared dependencies without limits, and autoscaling that adds load to a struggling dependency. *Avoid:* timeouts, backoff with jitter, retry budgets, circuit breakers, load shedding, bulkheads, and caps on concurrency into databases.

**16. Cluster sprawl and unclear ownership.** *What you see:* dozens of clusters nobody fully owns, inconsistent security, slow fixes. *Why:* clusters multiplied to limit blast radius without the automation to manage them. *Avoid:* treat clusters as rebuildable (Terraform plus GitOps), keep a fleet inventory and a single owner for each, upgrade and patch in waves, and enforce the same baseline with policy.

**The pattern.** Most of these are prevented by the same five habits: leave **headroom** below shared limits, set **limits and quotas** so one tenant cannot consume everything, keep the **blast radius** small (more clusters or cells), make every change **gradual with automated gates**, and **automate** operations so that a hundred clusters are managed like one.

## 5.6 Running data and analytics platforms on EKS (JupyterHub, Airflow, ShinyProxy, Immuta, Airbyte)

A platform that serves both microservices and data tools faces different demands from the two. Microservices are long-running, latency-sensitive and steady; data tools are bursty, long or interactive, memory-heavy, and often start one container per user or per job. This section explains how the tools named in the interviewer's description typically run, and the patterns that make them work on EKS. (Exact deployment details vary by version, so check each product's documentation.)

**JupyterHub (interactive notebooks).** A hub service authenticates users and, using a spawner for Kubernetes, starts a **separate pod per user** with that user's notebook server; a proxy routes the browser to the right pod. Idle notebooks are culled after a timeout to save cost. Per-user storage is a persistent volume (EBS is zone-bound; EFS is shared and flexible). Common issues: a user waits minutes for a pod because a node must be added and a large image pulled. The chart provides a placeholder mechanism: low-priority "user placeholder" pods hold spare capacity that real user pods displace immediately (the same technique as headroom pods in 6.1), combined with pre-pulled images and a node pool dedicated to users. Use on-demand nodes for interactive users (spot reclaims would kill sessions), and per-profile IAM roles so each team gets only its data.

**Airflow (workflow scheduling).** Components: a scheduler, a web server, a triggerer, a metadata database (a managed relational database, not a pod), and workers. With the **KubernetesExecutor**, each task runs as its own pod and disappears when done, so there are no idle workers; with the **CeleryExecutor**, long-lived workers pull tasks from a queue (and can be scaled by queue depth with KEDA, including to zero). DAG files arrive through a Git sync sidecar or a baked image; logs are shipped to object storage. Tasks must be idempotent and have retries, because spot interruptions and node scale-down can kill them. Put the scheduler and web server on stable on-demand nodes and task pods on spot or scale-from-zero node groups.

**ShinyProxy (hosting Shiny and other web apps).** A Java application that authenticates users and launches **one container per user session** for the requested app, using Docker or Kubernetes as the backend, then proxies the browser to it. It needs permission to create pods in a namespace (a tight RBAC role), sets idle timeouts, and benefits from placeholder capacity like JupyterHub. Network policies should prevent app pods from reaching anything except what they need.

**Immuta (data access governance).** A platform that enforces data access policies and masking on top of data sources so that users see only what they are allowed to. It is deployed as a set of services with state in databases; typical concerns are integration with the identity provider, network paths to the data stores, and the platform's own availability, because it sits in the data access path. Follow the vendor's Kubernetes deployment guide for sizing and storage.

**Airbyte (data ingestion).** A data integration tool with a server and workers that run **connector pods as jobs** for each sync, plus a workflow engine and a database. Scaling means more workers and capacity for job pods, which are memory-hungry for large syncs. Use dedicated, scale-from-zero node pools for sync jobs, object storage for logs and state, and retries.

**Patterns that apply to all of them.**

* **Node pools by workload type, separated with taints and labels:** a small stable pool (on-demand) for the platform's control services; user-facing interactive pools; batch pools (spot, scale from zero) with a taint that only tolerating pods accept.
* **Spot with care:** acceptable for retryable, checkpointed batch work; not for interactive sessions or single-copy services. Handle the two-minute warning, spread across instance types and zones, and set retries.
* **Scale to zero:** node groups scale to zero when no pods need them, and the autoscaler adds a node when a pod is pending. The trade-off is a startup delay (minutes) for the first job, which is fine for batch and bad for interactive use (use placeholders or a small warm pool there).
* **Storage:** EBS volumes are zone-bound, so pods are pinned to their zone; EFS or object storage (with a pod-identity role) removes that constraint.
* **Identity and data access:** an IAM role per team or user group through service accounts; governance tooling (such as Immuta) for fine-grained data policies; no long-lived keys in notebooks.
* **Isolation:** namespaces per team or tool, quotas, limit ranges, network policies, and pod security settings; users run arbitrary code, so assume untrusted workloads.
* **Cost controls:** culling idle sessions, scale to zero, spot where safe, quotas per team, and cost allocation labels per user or team.
* **Packaging:** charts supplied by the platform where possible, so every tool gets the same security, monitoring and labeling.

# Part 6: Autoscaling, headroom and Karpenter

## 6.1 Autoscaling for spiky login traffic (a morning peak or a retry storm)

Login traffic is bursty: many users authenticate at the start of a work day, and a failure that causes clients to retry multiplies load. The system must add capacity quickly, but capacity takes time to appear, so the design works at three levels at once: pods, nodes, and protection.

### Level 1: scaling pods with the HPA (and KEDA)

**What the HPA is.** The **Horizontal Pod Autoscaler (HPA)** is a Kubernetes controller that changes the *number of replicas* of a Deployment (more copies when busy, fewer when quiet). "Horizontal" means more copies, as opposed to "vertical" (bigger copies, which is the Vertical Pod Autoscaler's job). It runs a loop (every 15 seconds by default): read a metric, compare it with the target, compute the replica count it should have, and set it.

**The calculation.** Desired replicas = ceiling of (current replicas × current metric value ÷ target value). Example: 10 pods, each handling 100 requests per second on average, target 50 per pod: 10 × 100 ÷ 50 = 20 pods. The HPA ignores small differences (a 10 percent tolerance by default) so it does not twitch.

**What metric to use.** The HPA's classic metric is CPU utilization, measured as a percentage *of the pod's CPU request* (so requests must be set). CPU is a poor signal for many services: a login service can be saturated on a database or a thread pool while CPU is low, and CPU lags the load. A **request-based metric** means scaling on load directly, for example requests per second per pod, or concurrent requests in flight. To use one, the metric must be available to Kubernetes through the *custom metrics API* (for example Prometheus Adapter exposing a Prometheus query, or KEDA), or as an *external metric* (for example the load balancer's `RequestCountPerTarget` from CloudWatch).

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata: { name: login, namespace: auth }
spec:
  scaleTargetRef: { apiVersion: apps/v1, kind: Deployment, name: login }
  minReplicas: 6                    # at least two per zone across three zones
  maxReplicas: 60
  metrics:
    - type: Pods
      pods:
        metric: { name: http_requests_per_second }   # average per pod, from Prometheus via an adapter
        target: { type: AverageValue, averageValue: "50" }
  behavior:
    scaleUp:
      stabilizationWindowSeconds: 0                  # react immediately to rising load
      policies: [{ type: Percent, value: 100, periodSeconds: 30 }]   # at most double every 30 seconds
    scaleDown:
      stabilizationWindowSeconds: 300                # wait 5 minutes of lower demand before shrinking
      policies: [{ type: Pods, value: 2, periodSeconds: 60 }]        # remove at most 2 pods per minute
```

**The `behavior` section** controls speed. Scale up fast (protect users) and scale down slowly (avoid removing capacity just before the next burst). The *stabilization window* makes the HPA take the highest recommendation over the window when scaling down, which prevents flapping. The *policies* cap how many pods or what percentage can change per period.

**KEDA, and why it is used.** **KEDA (Kubernetes Event-Driven Autoscaling)** adds scalers for things the HPA does not understand natively: the length of an SQS queue or Kafka topic lag, a Prometheus query, a cron schedule, a database row count, and dozens more. You define a `ScaledObject`; KEDA creates and manages an HPA for it and feeds it the metric. Its distinctive feature is **scaling to and from zero**: a plain HPA cannot go below one replica, whereas KEDA can scale a worker deployment to zero when the queue is empty and start it again when messages arrive.

```yaml
apiVersion: keda.sh/v1alpha1
kind: ScaledObject
metadata: { name: worker, namespace: data }
spec:
  scaleTargetRef: { name: worker }
  minReplicaCount: 0            # scale to zero when idle
  maxReplicaCount: 50
  cooldownPeriod: 300           # wait before scaling back to zero
  triggers:
    - type: aws-sqs-queue
      metadata:
        queueURL: https://sqs.us-east-1.amazonaws.com/111122223333/jobs
        queueLength: "20"       # target number of messages per replica
        awsRegion: us-east-1
```

**Which to choose.** HPA with a request-rate metric for synchronous services such as login; KEDA for event-driven workers and anything that should scale to zero.

### Level 2: scaling nodes, and the headroom problem

More pods need nodes to run on. New nodes take time (from tens of seconds to a few minutes: launch the instance, boot, join the cluster, pull images), so reacting only after pods go pending means users wait. Two tools handle node capacity:

* **Karpenter** watches for pending pods and launches the cheapest nodes that fit, directly through EC2, usually within a minute or two. It also removes idle nodes (consolidation).
* **Cluster Autoscaler** works with predefined node groups (Auto Scaling groups): when pods cannot be scheduled it increases the size of a suitable group; when nodes are underused (by default below about 50 percent utilization for 10 minutes) and their pods can move elsewhere, it removes them. It can scale a group to zero if it knows what the group's nodes would look like (the group carries tags describing its labels and taints). It is slower and less flexible than Karpenter, and a group per zone is recommended when volumes are zone-bound.

**Headroom pods: how to hold spare capacity that real pods can take instantly.** The idea: keep some nodes running with spare room by running *placeholder pods* that do nothing but reserve capacity. When a real pod needs the room, Kubernetes evicts a placeholder (instantly) and the real pod starts immediately; the evicted placeholder becomes pending, which triggers the node autoscaler to add a node in the background, restoring the headroom. Users never wait for a node to boot.

This works through **pod priority**. Kubernetes has a `PriorityClass` object that maps a name to an integer *priority value*. Every pod can name a `priorityClassName` in its spec. The scheduler considers higher-priority pods first and, if a high-priority pod cannot fit anywhere, it **preempts** (evicts) lower-priority pods to make room. Priority also affects which pods are evicted first when a node is under pressure. So you create a very low priority class for the placeholders, and leave real workloads at the default priority (0) or a higher class:

```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata: { name: overprovisioning }
value: -10                           # lower than the default (0): real pods always win
globalDefault: false
description: "Placeholder pods that real workloads may preempt"
---
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata: { name: production-critical }
value: 1000000                       # for services that must be scheduled before others
---
apiVersion: apps/v1
kind: Deployment
metadata: { name: headroom, namespace: kube-system }
spec:
  replicas: 5                        # 5 placeholders x 2 CPU / 4 GiB = 10 CPU and 20 GiB spare
  selector: { matchLabels: { app: headroom } }
  template:
    metadata: { labels: { app: headroom } }
    spec:
      priorityClassName: overprovisioning
      terminationGracePeriodSeconds: 0     # evict instantly
      containers:
        - name: pause
          image: registry.k8s.io/pause:3.9   # a tiny container that does nothing
          resources:
            requests: { cpu: "2", memory: 4Gi }   # the amount of spare room each placeholder reserves
```

A real service opts into a priority by setting `priorityClassName: production-critical` in its pod template (and a platform can restrict who may use high classes with a ResourceQuota scoped to priority class). Sizing the headroom: estimate the burst you must absorb before new nodes arrive (for example the extra pods for two minutes of growth) and multiply by pod requests. The trade-off is cost: you pay for the idle spare capacity, so size it to the burst, and put it only where startup delay matters.

### Level 3: protection and dependencies

* **Shed load and limit abuse at the edge:** rate limits per client and per tenant (web application firewall rules), so a retry storm or an attack does not become the platform's problem. When the system is overloaded, reject excess requests early with a fast error instead of queueing them until everything times out.
* **Scheduled pre-scaling** before known peaks (raise the HPA minimum before the morning peak), since predicting beats reacting.
* **Protect the database:** the true limit is often the single large database per cell, which cannot scale out. Cap concurrency from each service, use connection pooling or RDS Proxy, add caching for hot reads, and make sure scaling pods up does not open thousands of extra connections.
* **Fast startup:** small images, pre-pulled images on nodes, tuned probes, so a new pod serves traffic in seconds.
* **Keep replicas spread across zones** with topology spread, and keep a PodDisruptionBudget, so scale-in and node consolidation do not drop capacity at the wrong moment.

**Test it.** A load test that includes a sharp ramp, a node scale-out, and the loss of a zone, measuring time to add capacity and the error rate during the ramp. Tune the HPA behavior, headroom size and minimums from the results.

## 6.2 Managing pod scaling in day-to-day operations

**Reading the HPA's own explanation.** `kubectl get hpa -w` shows current versus target and replica counts; `kubectl describe hpa NAME` shows *conditions* (`AbleToScale`, `ScalingActive`, `ScalingLimited`) and events with reasons. If `ScalingActive` is false with a message about missing metrics, the HPA cannot compute anything.

**Common HPA problems and their causes.**

| Symptom | Cause | Fix |
| :--- | :--- | :--- |
| Target shows `<unknown>/50%` | The metrics server is not installed or unhealthy; the pod has no CPU request (utilization is a percentage of the request); the custom metrics adapter is misconfigured | Install and check `kubectl top pods`; set requests; verify the metric exists through the metrics API |
| Never scales up | Metric below target; maximum replicas reached (`ScalingLimited`); quota or node capacity blocks new pods | Check the metric, raise the maximum, check Pending pods and quotas |
| Flapping (up and down repeatedly) | Metric oscillates; stabilization window too short; a metric affected by scaling itself | Lengthen scale-down stabilization, choose a steadier metric, limit step size |
| Scales too slowly for spikes | Metrics lag (scrape and aggregation intervals), policies cap increases, nodes slow to appear | Faster metric, larger scale-up policy, headroom pods (6.1), pre-scaling |
| Replicas keep resetting | A GitOps tool or a manifest sets `replicas` and fights the HPA | Remove `replicas` from the Deployment manifest when an HPA owns it, or tell the GitOps tool to ignore that field |
| Pods start but traffic fails | New pods receive traffic before ready | Correct readiness probe and warm-up |

**Right-sizing requests (the foundation of good scaling).** Utilization-based scaling and node packing both depend on accurate CPU and memory requests. The **Vertical Pod Autoscaler (VPA)** watches actual usage and recommends requests. Its modes: *Off* (recommendations only, safe to start with), *Initial* (sets requests at pod creation), and *Auto* or *Recreate* (evicts pods and recreates them with new requests, which causes restarts). A good practice is to run VPA in recommendation mode, review the numbers regularly and update the chart values. Do not let VPA and HPA both act on CPU for the same workload, because they will fight.

**Manual and scheduled scaling.** `kubectl scale deployment/NAME --replicas=N` sets replicas immediately (useful in incidents; remember that an HPA or GitOps tool may override it). Scheduled scaling for known peaks can be done with KEDA's cron scaler or by raising the HPA's minimum before the peak. When capacity must be guaranteed, scale up before the event, not during.

**Scaling limits to configure on purpose.** Minimum replicas (at least the number of zones, for availability); maximum replicas (a cost and dependency safety limit); namespace quotas (so one team cannot scale the cluster into exhaustion); and node pool limits (Karpenter limits). Protect dependencies by capping how fast and how far services scale relative to what the database can accept.

**Scaling and disruption together.** PodDisruptionBudgets and topology spread keep availability during scale-in and node consolidation; graceful shutdown prevents errors when pods are removed.

## 6.3 Karpenter in depth

**What it does.** Karpenter watches for pods that cannot be scheduled, works out the cheapest suitable instance types, and launches nodes directly through EC2 in seconds to a minute or two. It also removes or replaces nodes that are underused. The Cluster Autoscaler, by contrast, resizes predefined Auto Scaling groups and is slower and less flexible.

**The two main objects.**

* **NodePool:** what kind of nodes may be created: allowed instance categories and sizes, architecture (x86 or ARM), capacity type (on-demand or spot), zones, labels and taints, a **limit** on total CPU and memory (a cost safety net), and **disruption** rules (when and how nodes may be consolidated or replaced, plus disruption budgets that cap how many at once).
* **EC2NodeClass:** the AWS specifics: image family, subnets and security groups (selected by tags), the node's IAM role, disk settings and startup script.

**Behaviors to explain.**

* **Bin-packing:** picks nodes that fit pending pods snugly, which is why correct pod *requests* matter.
* **Consolidation:** deletes or replaces nodes that are empty or can be packed better; this saves money but evicts pods, so PodDisruptionBudgets, graceful shutdown and replicas are essential.
* **Drift and expiration:** when the node image or NodePool changes, or a node reaches a maximum age, Karpenter replaces nodes gradually. This gives you rolling patching, but pin image versions so a surprise new image is not rolled out everywhere at once.
* **Interruption handling:** with an interruption queue fed by EventBridge, Karpenter reacts to spot interruption warnings and other events by draining and replacing nodes early.
* **Do-not-disrupt annotation:** protects pods (for example a long job) from voluntary eviction.
* **Headroom:** low-priority placeholder pods keep spare capacity that real pods preempt, so spikes do not wait for node startup (how this works with priority classes, with YAML, is in 6.1).

**Pitfalls.** Pods with unsatisfiable requirements stay pending (read the Karpenter logs and events); aggressive consolidation causes churn; many small nodes hit network address and card limits; spot with single-replica workloads causes outages; subnets running out of addresses; slow node startup from large images (pre-pull or use a pull-through cache); and forgetting that DaemonSets consume part of every node.

### 6.3.1 Configuring and using Karpenter, step by step

**What you set up once.**

1. **Install the controller** with its Helm chart into a namespace such as `kube-system` (or its own). Run it on a stable node group (a small managed node group or Fargate), never on nodes it controls, because a controller that can be scaled away cannot bring nodes back.
2. **Give it AWS permissions.** The controller needs an IAM role (through IRSA or EKS Pod Identity) allowing it to launch and terminate EC2 instances, read pricing and instance types, read SSM parameters for images, and pass the node role. Nodes need their own *node role* (the standard worker permissions, including pulling images) that Karpenter attaches.
3. **Tag what Karpenter may use.** Subnets and security groups carry a discovery tag (for example `karpenter.sh/discovery: my-cluster`) so Karpenter knows where nodes may be placed.
4. **Create an interruption queue** (an SQS queue fed by EventBridge rules) so Karpenter hears about spot interruption warnings, instance health events and rebalance recommendations and can drain nodes early.
5. **Define node classes and node pools** (below). Without a NodePool, Karpenter does nothing.

**EC2NodeClass: the AWS-specific recipe for a node.**

```yaml
apiVersion: karpenter.k8s.aws/v1
kind: EC2NodeClass
metadata: { name: default }
spec:
  role: KarpenterNodeRole-my-cluster               # IAM role for the nodes
  amiSelectorTerms:
    - alias: bottlerocket@latest                   # pin a specific version in production, not "latest"
  subnetSelectorTerms:
    - tags: { karpenter.sh/discovery: my-cluster } # which subnets nodes may use
  securityGroupSelectorTerms:
    - tags: { karpenter.sh/discovery: my-cluster }
  metadataOptions:                                 # IMDSv2 only, hop limit 1
    httpTokens: required
    httpPutResponseHopLimit: 1
  blockDeviceMappings:
    - deviceName: /dev/xvda
      ebs: { volumeSize: 50Gi, volumeType: gp3, encrypted: true }
  tags: { team: platform, cost-center: infra }
```

**NodePool: what kinds of nodes may exist, and how they may be removed.**

```yaml
apiVersion: karpenter.sh/v1
kind: NodePool
metadata: { name: general }
spec:
  template:
    spec:
      nodeClassRef: { group: karpenter.k8s.aws, kind: EC2NodeClass, name: default }
      requirements:
        - { key: karpenter.sh/capacity-type, operator: In, values: ["on-demand"] }
        - { key: kubernetes.io/arch, operator: In, values: ["amd64", "arm64"] }
        - { key: karpenter.k8s.aws/instance-category, operator: In, values: ["c", "m", "r"] }
        - { key: karpenter.k8s.aws/instance-generation, operator: Gt, values: ["4"] }
        - { key: topology.kubernetes.io/zone, operator: In, values: ["us-east-1a", "us-east-1b", "us-east-1c"] }
      expireAfter: 720h                    # replace nodes older than 30 days (rolling patching)
  limits:
    cpu: "2000"                            # cost safety net: never exceed 2000 vCPUs in this pool
    memory: 8000Gi
  disruption:
    consolidationPolicy: WhenEmptyOrUnderutilized
    consolidateAfter: 5m
    budgets:
      - nodes: "10%"                       # at most 10% of nodes disrupted at once
      - nodes: "0"                         # no voluntary disruption on weekday mornings
        schedule: "0 8 * * mon-fri"
        duration: 3h
---
apiVersion: karpenter.sh/v1
kind: NodePool
metadata: { name: batch-spot }
spec:
  weight: 10
  template:
    spec:
      nodeClassRef: { group: karpenter.k8s.aws, kind: EC2NodeClass, name: default }
      requirements:
        - { key: karpenter.sh/capacity-type, operator: In, values: ["spot"] }
        - { key: karpenter.k8s.aws/instance-category, operator: In, values: ["c", "m", "r"] }
      taints:
        - { key: workload, value: batch, effect: NoSchedule }   # only pods that tolerate this land here
  limits: { cpu: "1000" }
  disruption: { consolidationPolicy: WhenEmptyOrUnderutilized, consolidateAfter: 1m }
```

*(API versions and some field locations changed between Karpenter releases, so check the documentation for the version you install.)*

**How workloads use it.** Pods do not "ask for Karpenter." They express needs, and Karpenter provisions what satisfies them:

* **Resource requests** (CPU, memory) decide how big the nodes must be. Accurate requests are the single biggest factor in cost and fit.
* **`nodeSelector`, affinity and tolerations** choose pools: a batch pod adds `tolerations` for the batch taint and `nodeSelector: { karpenter.sh/capacity-type: spot }`.
* **Topology spread constraints** make Karpenter place nodes in several zones.
* **`karpenter.sh/do-not-disrupt: "true"`** on a pod (or node) protects it from voluntary disruption such as consolidation.
* **Several pools** separate concerns: general on-demand, spot for batch, GPU, a pool for the platform's own pods; the `weight` field sets preference when several pools could satisfy a pod.

**How the lifecycle looks.** A pod goes Pending, Karpenter evaluates all pending pods together, picks the cheapest instance types that satisfy them (bin-packing), creates a **NodeClaim**, EC2 launches the instance, the node joins and becomes Ready, the scheduler places the pod. Later, consolidation notices underused or empty nodes and removes or replaces them within the disruption budgets; drift replaces nodes whose configuration changed; expiry replaces old nodes.

**Operating it.**

* Look at state with `kubectl get nodepools,nodeclaims,ec2nodeclasses` and `kubectl describe nodeclaim NAME`; read the controller logs and events for decisions (why a node was created or why a pod could not be scheduled).
* Watch its Prometheus metrics: NodeClaims created and terminated, pod startup latency, disruption decisions, and pool usage against limits.
* Upgrade it deliberately (apply updated CRDs first, move within the compatibility matrix with your Kubernetes version), canary cluster first.
* Control cost: diversify instance types (a wide set lowers spot interruption), set limits, use Graviton where software supports it, and choose consolidation settings that match your tolerance for churn.

**Troubleshooting checklist.**

| Symptom | Check |
| :--- | :--- |
| Pods Pending and no NodeClaim | No NodePool matches the pod (requirements, taints or selectors conflict), or pool limits reached; read the controller log message |
| NodeClaim created but node never ready | Missing or wrong node role, security group or subnet tags, no free IPs in the subnet, image or user data problem |
| "Insufficient capacity" errors | Instance types too narrow or spot unavailable; widen the instance list and zones |
| Constant node churn | Consolidation too aggressive, pods without disruption budgets, spot interruptions on single-replica services |
| Nodes not replaced during drift or expiry | A PodDisruptionBudget or do-not-disrupt annotation is blocking, or the disruption budget is zero |
| Cost higher than expected | Over-large requests, daemon overhead, limits too high, unused pools, on-demand where spot is acceptable |

# Part 7: Delivery: Helm, Spinnaker and GitOps

## 7.1 Helm in depth: charts, version files, values and releases

**What Helm is.** Helm is the package manager for Kubernetes. A **chart** is a package of Kubernetes templates plus default settings. You install a chart with your own values and get a **release**: a named, versioned instance of that chart in a cluster. Helm keeps a history of each release so you can inspect and roll back.

**What is in a chart.**

```text
platform-service/
  Chart.yaml            # metadata: the chart's name and version, and the version of the app inside
  Chart.lock            # the exact versions of dependencies that were resolved (generated)
  values.yaml           # default settings
  values.schema.json    # optional: validates values (types, required fields, allowed values)
  templates/            # Kubernetes YAML with Go templating: deployment.yaml, service.yaml, hpa.yaml...
    _helpers.tpl        # reusable template snippets
    NOTES.txt           # text printed after install
  charts/               # downloaded dependency charts (subcharts)
  crds/                 # CustomResourceDefinitions installed first (Helm does not upgrade or delete these)
```

**The "version file": `Chart.yaml`.** This is the file people usually mean. Its important fields:

```yaml
apiVersion: v2                # chart format (v2 is Helm 3)
name: platform-service
description: Standard deployment chart for stateless services
type: application             # or "library" (reusable templates, no resources of its own)
version: 2.4.1                # the CHART version (semantic versioning)
appVersion: "1.8.3"           # the version of the APPLICATION packaged (informational; often the default image tag)
kubeVersion: ">=1.28.0-0"     # which Kubernetes versions the chart supports
dependencies:
  - name: common
    version: "1.x.x"          # a version constraint
    repository: oci://registry.example.com/charts
```

The two versions answer different questions: **`version`** is the version of the *packaging* (the templates and defaults). Bump it whenever anything in the chart changes, even if the app did not. **`appVersion`** is the version of the *software* being deployed. They move independently: changing a probe default is a chart bump (2.4.1 to 2.5.0) with the same appVersion; shipping a new application release changes the image tag (appVersion 1.8.4) and may or may not require a chart bump.

**Other "version" things people mean, and how to tell them apart.**

| What | Where | Meaning |
| :--- | :--- | :--- |
| `helm version` | command | Version of the Helm client program itself (for example v3.x) |
| Chart `version` | Chart.yaml | Version of the chart package |
| `appVersion` | Chart.yaml | Version of the packaged application |
| `Chart.lock` | file next to Chart.yaml | Exact resolved versions (and a digest) of dependencies, produced by `helm dependency update`; like a lockfile in other package managers; commit it so builds are repeatable |
| Release **revision** | `helm history RELEASE` | An integer that increases with every install, upgrade and rollback of one release in one cluster |
| Repository index | `index.yaml` in a chart repository (or tags in an OCI registry) | The list of chart versions available |

**Values: how settings are combined.** Default `values.yaml` in the chart, overridden by values files given with `-f` (later files override earlier ones), overridden by `--set` on the command line. A parent chart can also set values for its subcharts. The usual practice: the chart ships safe defaults, and each environment or cluster supplies a small values file (`values-prod-cell-101.yaml`). Use `values.schema.json` to reject invalid values at install time.

**Releases and where Helm stores them.** Helm 3 stores each revision of a release as a Kubernetes Secret in the release's namespace (named like `sh.helm.release.v1.orders.v7`), containing the rendered manifest and the values used. That is why `helm history`, `helm get values`, `helm get manifest` and `helm rollback` work. An upgrade compares three things (the previous release's manifest, the live objects, and the new manifest) and patches the difference. A rollback creates a *new* revision that restores an older manifest; it does not rewind the counter. By default Helm keeps the last ten revisions.

**The commands you should know.**

```bash
helm lint ./platform-service                       # check the chart for problems
helm template orders ./platform-service -f values.yaml   # render locally, no cluster needed
helm install orders ./platform-service -n shop -f values.yaml
helm upgrade --install orders ./platform-service -n shop -f values.yaml --version 2.4.1 --atomic --wait --timeout 5m
helm history orders -n shop                        # list revisions and their status
helm rollback orders 6 -n shop                     # go back to the manifest of revision 6
helm get values orders -n shop                     # the values the release used
helm diff upgrade orders ./platform-service -f values.yaml   # preview changes (plugin)
helm dependency update ./platform-service          # download dependencies and write Chart.lock
helm package ./platform-service && helm push platform-service-2.4.1.tgz oci://registry.example.com/charts
```

`--atomic` rolls back automatically if the upgrade fails; `--wait` waits until resources are ready. `helm template | kubeconform` in CI catches invalid manifests before any cluster is touched.

**Hooks and tests.** Annotations such as `helm.sh/hook: pre-upgrade` run a Job at a specific point (a database migration before the new version starts); `helm test` runs test pods. Hooks are powerful and risky (a failing hook blocks the release; hooks are not part of the normal release object), so keep them few.

**Common problems and fixes.**

* **Release stuck in `pending-upgrade` or `failed`:** an interrupted or failed upgrade. Check `helm history`; roll back to the last good revision, or fix and re-run with `--atomic`. Concurrent upgrades of the same release cause this too, so serialize them in the pipeline.
* **"Field is immutable":** a change to something Kubernetes will not alter in place (a Deployment's selector, a Job's template). Delete and recreate, or avoid changing it.
* **CRD changes not applied:** Helm installs CRDs from `crds/` once and does not upgrade them; manage CRD upgrades separately (a dedicated chart or a GitOps step).
* **Surprise upgrades:** deploying "the latest chart" or a loose constraint like `2.x` can change behavior unexpectedly. Always pin the exact chart version in what you deploy, and bump it deliberately through review.
* **Huge releases:** release Secrets have a size limit, so very large charts or many subcharts can fail to store; split them.
* **Drift:** someone edits objects by hand; Helm's three-way merge may keep or revert changes unpredictably. Use GitOps (for example Argo CD) or restrict manual edits.
* **Secrets in values:** values are stored in the release Secret and often in Git; reference an external secret instead of placing plaintext values.

**Say it like this.** "The chart's `version` in Chart.yaml versions the packaging and the `appVersion` versions the application; I pin the exact chart version per cluster, keep per-cluster values in a small file, use `--atomic` for safe upgrades, and rely on `helm history` and `helm rollback` when something goes wrong."

## 7.2 Platform-provided Helm charts ("golden charts")

**What it is.** Instead of every team writing its own Kubernetes YAML, the platform team publishes a small number of **versioned Helm charts** (for a stateless web service, a worker, a job, a cron job) that encode all the standards: probes, resource requests, topology spread, pod disruption budget, restricted security context, service account, network policy, ingress, autoscaler, monitoring hooks and cost labels. A team deploys its service by supplying only **values**: the image, a few settings, and its environment.

**Why it works.** It reduces what a team must know, makes the safe configuration the default, and lets the platform improve every service at once: release chart version 2.5 with a better default, and teams pick it up by changing a version number. It also gives the platform a clear contract to measure and support.

**How to design it well.**

* **A small, stable values interface,** documented, with a `values.schema.json` that validates inputs (wrong types or forbidden settings fail at install time instead of in production).
* **Opinionated defaults with controlled escape hatches:** most settings are not exposed; a few (extra containers, custom annotations) are, with review.
* **Semantic versioning:** a major version for breaking changes; deprecation notices and migration guides; a support window for older majors.
* **Tested in CI:** render the chart with sample values, validate against the Kubernetes schemas and policies, deploy to a test cluster.
* **Consumed through GitOps:** each service is described by an Argo CD Application, or by a Spinnaker pipeline run from a per-cluster file (see Spinnaker), that references the chart version and carries the service's own values.
* **Upgrades in rings:** the platform releases a new chart version, a canary set of services adopts it first, then it spreads. Automated pull requests propose the version bump to every consumer.

```yaml
# a service team's whole deployment definition: a small Argo CD Application that points at the platform chart
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: { name: orders, namespace: argocd }
spec:
  project: shop
  destination: { server: https://kubernetes.default.svc, namespace: shop }
  source:
    repoURL: https://charts.example.com        # the platform's chart repository
    chart: platform-service
    targetRevision: 2.4.1                      # exact chart version, bumped through review
    helm:
      values: |
        image: { repository: 111122223333.dkr.ecr.us-east-1.amazonaws.com/orders, tag: 1.8.3 }
        replicas: 3
        resources: { requests: { cpu: 500m, memory: 512Mi } }
        ingress: { enabled: true, host: orders.example.com }
        secrets: [ { name: db-password, source: orders/db } ]
  syncPolicy: { automated: { prune: true, selfHeal: true } }
```

**Trade-offs.** A chart that tries to serve every case becomes a template with a hundred options; one that is too rigid is bypassed. Keep a few chart types, listen to teams, and add features only when several teams need them. A breaking change in a platform chart affects every consumer, so treat it as a product release.

## 7.3 GitOps with Argo CD

**GitOps** means Git is the source of truth for what runs in a cluster: you change a file in Git, and a controller running in the cluster pulls the change and applies it (and can revert manual drift). Argo CD is the GitOps controller covered here; Spinnaker, covered next, takes a different, pipeline-driven approach, and the two are compared in 7.5.

* **Argo CD** continuously compares the cluster with Git and syncs it. Know: **Application** (one deployment), **AppProject** (boundaries and permissions), **ApplicationSet** (generates many applications from a list of clusters, environments or cells), **app of apps** (a root application that deploys others), **sync waves and hooks** (ordering: CRDs before resources that use them), **auto-sync, self-heal and prune** (revert manual drift, delete what was removed from Git), **ignoreDifferences** (for fields other controllers change), and controller sharding for scale. One Argo per cluster (pull model) keeps blast radius small; a central Argo managing many clusters is simpler to see but a bigger target.
* **Helm versus Kustomize.** Helm packages with templated values and release history; Kustomize layers patches over a base with no templating. Many teams use Helm for third-party software and Kustomize or values files for their own; avoid deep templating. Use `helm diff` before upgrades, pin chart versions, and know `helm history` and `helm rollback`.
* **Promotion.** Repository layout with a base and per-environment or per-cell overlays; the same image promoted through environments by pull request or automation, never rebuilt.
* **Secrets.** Never plaintext in Git: External Secrets Operator (reads AWS Secrets Manager or Parameter Store), SOPS or Sealed Secrets.
* **Checks before merge:** manifest validation (kubeconform), policy tests (OPA conftest or Kyverno CLI), image scanning. In the cluster, admission policy enforces the same rules.
* **Argo CD versus Spinnaker:** a detailed comparison follows in 7.5.

## 7.4 Spinnaker: everything in one place

### What Spinnaker is, and its vocabulary

Spinnaker is an open-source continuous delivery platform created at Netflix. It does **delivery**, not building: a CI system (Jenkins, GitHub Actions) builds and tests the code and produces an artifact (an image, a Helm chart); Spinnaker takes that artifact through stages that deploy and verify it.

* **Application:** a logical grouping in Spinnaker (for example "orders") that holds pipelines and shows what is deployed where.
* **Account:** a connection to a deployment target. For Kubernetes, **one account is one cluster** (a kubeconfig or IAM-based credential). Clouddriver, the component that talks to clusters, uses accounts.
* **Pipeline:** an ordered, branching workflow of **stages** (bake, deploy, wait, approve, test, roll back).
* **Trigger:** what starts a pipeline: a new image in a registry, a Git push, a Jenkins build finishing, a cron schedule, a **webhook** (an HTTP call from another system), or another pipeline.
* **Parameters:** inputs supplied when a pipeline starts (manually, from a webhook or from another pipeline).
* **Artifacts:** the files and references a pipeline uses: a Helm chart, a values file, a manifest, an image.
* **Pipeline expressions:** values computed at run time with the Spring Expression Language, written `${ ... }`, for example `${trigger.payload.cluster}` (a field in the webhook that started this run) or `${parameters.version}`.
* **Components:** Orca (runs pipelines), Clouddriver (talks to clusters and clouds), Gate (the API and gateway), Deck (the UI), Echo (triggers and notifications), Igor (CI integration), Front50 (stores definitions), Fiat (authorization), Rosco (bakes manifests and images), Kayenta (automated canary analysis).

### How a Helm deployment runs in Spinnaker

Spinnaker does not run `helm install`. It **renders** the chart to plain Kubernetes manifests and applies them:

1. **Bake (Manifest) stage with the Helm 3 renderer.** Inputs: the chart (an artifact from a chart repository, Git or S3), optional values files, and key-value overrides. Output: a *baked manifest* artifact.
2. **Deploy (Manifest) stage.** Applies the baked manifest to a chosen account (cluster) and namespace, with a strategy (rolling, or red/black for blue/green behind a load balancer) and an option to **wait for the manifest to stabilize** (so the stage fails if pods never become ready).
3. **Verify.** Smoke tests (a Run Job stage or a webhook stage) or automated canary analysis with Kayenta.
4. **Approve or continue.** A manual judgment, a wait, or the next stage.
5. **Roll back on failure.** An Undo Rollout stage, usually triggered by a failed stage.

Because the chart is rendered, **no Helm release object exists in the cluster** for Spinnaker-deployed charts, so `helm list` shows nothing; Spinnaker's own view and the resources' labels (such as `helm.sh/chart`, which carries the chart name and version) tell you what is deployed.

### Deploying different Helm versions to many clusters with ONE common pipeline (Pattern B)

**The requirement.** You have many clusters (for example `prod-cell-101`, `prod-cell-102`, `prod-cell-103`). Each may run a different chart or application version and have different values. You want:

* **one pipeline** (written once, maintained once) that deploys to any cluster;
* **per-cluster configuration kept as data** in Git, reviewed through pull requests;
* when someone changes `prod-cell-102.yaml`, **only cluster 102 is deployed**, and the other clusters are not touched and no pipeline runs for them.

**The key idea.** Spinnaker should not decide *which* clusters changed. A small step in front of Spinnaker (the "change detector") works that out from Git and starts **one pipeline execution per changed cluster**, passing that cluster's settings as input. The pipeline itself is generic: it deploys whatever cluster and version it is told to.

**Step 1: the configuration repository.**

```text
fleet-config/
  clusters/                 one small file per cluster: WHAT should run there
    prod-cell-101.yaml
    prod-cell-102.yaml
    staging-cell-s01.yaml
  values/                   one Helm values file per cluster: HOW it is configured
    prod-cell-101.yaml
    prod-cell-102.yaml
  shared/
    base-values.yaml        settings common to every cluster
  rings.yaml                which cluster belongs to which rollout ring
```

```yaml
# clusters/prod-cell-102.yaml
cluster: prod-cell-102
account: eks-prod-cell-102       # the Spinnaker account for this cluster
namespace: shop
chart: platform-service
chartVersion: 2.5.0              # the version this cluster should run
imageTag: 1.8.4
ring: early
```

Values are layered the usual Helm way: the chart's defaults, then `shared/base-values.yaml`, then `values/<cluster>.yaml`, then the key-value overrides from the pipeline (the image tag).

**Step 2: the change detector (runs in CI, for example GitHub Actions).** It runs when a pull request is merged. It lists the files that changed, turns them into a list of cluster names, and starts Spinnaker once per cluster.

```yaml
name: deploy-changed-clusters
on:
  push:
    branches: [main]
    paths: ['clusters/**', 'values/**']
jobs:
  detect:
    runs-on: ubuntu-latest
    outputs:
      clusters: ${{ steps.changed.outputs.clusters }}
    steps:
      - uses: actions/checkout@v4
        with: { fetch-depth: 0 }
      - id: changed
        run: |
          names=$(git diff --name-only "${{ github.event.before }}" "${{ github.sha }}" -- clusters/ values/ \
            | sed -E 's#^(clusters|values)/([^/]+)\.ya?ml$#\2#' | sort -u)
          keep=""
          for n in $names; do [ -f "clusters/$n.yaml" ] && keep="$keep $n"; done   # ignore files that are not a cluster
          json=$(printf '%s\n' $keep | jq -R . | jq -sc 'map(select(length>0))')
          echo "clusters=$json" >> "$GITHUB_OUTPUT"

  deploy:
    needs: detect
    if: needs.detect.outputs.clusters != '[]'
    runs-on: ubuntu-latest
    strategy:
      matrix:
        cluster: ${{ fromJson(needs.detect.outputs.clusters) }}
      max-parallel: 5
    concurrency:
      group: spinnaker-${{ matrix.cluster }}     # never run two deployments for the same cluster at once
      cancel-in-progress: false
    steps:
      - uses: actions/checkout@v4
      - name: Start the common Spinnaker pipeline for ${{ matrix.cluster }}
        env:
          CLUSTER: ${{ matrix.cluster }}
        run: |
          payload=$(yq -o=json '.' "clusters/${CLUSTER}.yaml" | jq --arg commit "$GITHUB_SHA" '. + {commit: $commit}')
          curl -sS --fail -X POST "$SPINNAKER_GATE/webhooks/webhook/fleet-deploy" \
            -H "Content-Type: application/json" -d "$payload"
```

What this does when you change `clusters/prod-cell-102.yaml`: the `detect` job finds exactly one changed file, derives the name `prod-cell-102`, outputs `["prod-cell-102"]`; the `deploy` job runs a matrix of one entry, reads `clusters/prod-cell-102.yaml` and posts its contents (plus the commit SHA) to Spinnaker. No other cluster is mentioned, so no other execution exists. If a pull request changes two cluster files, you get two executions, one per cluster. If someone edits `values/prod-cell-102.yaml` only, the same logic selects cluster 102 (the sed rule maps both directories to the cluster name).

**Step 3: the one common pipeline (`fleet-deploy`).** It has a **webhook trigger**, so everything it needs arrives in `trigger.payload`:

```json
{
  "triggers": [
    { "type": "webhook", "enabled": true, "source": "fleet-deploy",
      "payloadConstraints": { "cluster": ".+", "chartVersion": "^[0-9]+\\.[0-9]+\\.[0-9]+$" } }
  ]
}
```

(The payload constraints make Spinnaker ignore calls that lack a cluster or a valid chart version.) The stages, in order:

| # | Stage (type) | What it does | Key settings |
| :--- | :--- | :--- | :--- |
| 1 | Validate (Check Preconditions) | Fails fast on bad input | Expressions such as `${trigger.payload.cluster != null}` and `${trigger.payload.ring in {'canary','early','broad','critical'}}` |
| 2 | Bake chart (Bake Manifest, Helm 3) | Renders the chart at the cluster's pinned version with its values | Chart artifact name `${trigger.payload.chart}`, version `${trigger.payload.chartVersion}`; values artifacts `shared/base-values.yaml` then `values/${trigger.payload.cluster}.yaml`, both read from the repository at commit `${trigger.payload.commit}`; overrides `image.tag=${trigger.payload.imageTag}` |
| 3 | Approval (Manual Judgment) | Human gate for sensitive rings | Run only when `${trigger.payload.ring == 'critical'}` (conditional on expression) |
| 4 | Deploy (Deploy Manifest) | Applies the baked manifest to this cluster | Account `${trigger.payload.account}`, namespace `${trigger.payload.namespace}`, wait for the manifest to stabilize; on failure, ignore so the rollback stage can run |
| 5 | Verify (Run Job or Webhook, optionally canary analysis) | Smoke test against this cluster's endpoint, or compare canary metrics for the canary ring | Endpoint built from the cluster name, for example `https://${trigger.payload.cluster}.example.com/healthz` |
| 6 | Roll back (Undo Rollout) | Restores the previous version if deploy or verify failed | Run only when `${#stage('Deploy')['status'].toString() == 'TERMINAL'}` (or the verify stage failed) |
| 7 | Fail the pipeline if rolled back | Makes the execution show as failed, so alerts and the CI job see it | Conditional on the same expression |
| 8 | Record (Webhook) | Posts the result and the version to a deployment record or sets a commit status | Cluster, version, outcome, execution link |

*(Stage names and field labels vary by Spinnaker version. In many versions the account and namespace fields accept expressions. If yours does not, see "Other patterns" below.)*

**Step 4: the walkthrough.** A team wants cluster 102 to move from chart 2.4.1 to 2.5.0 and image 1.8.4:

1. Engineer opens a pull request changing `chartVersion` and `imageTag` in `clusters/prod-cell-102.yaml`.
2. CI on the pull request validates the file (schema, the chart version exists in the chart repository, the account exists). Code owners approve (production cells require two approvals).
3. The pull request is merged. The change detector outputs `["prod-cell-102"]` and starts one execution of `fleet-deploy` with that cluster's settings.
4. Spinnaker bakes chart 2.5.0 with the layered values, deploys to the account `eks-prod-cell-102`, waits for pods to become ready, runs the smoke test, and records success. Clusters 101 and 103 continue running whatever they were running; nothing was triggered for them.
5. The commit status and the Spinnaker execution link show the result. If verification fails, the rollback stage restores the previous revision and the pipeline ends in a failed state.

**What if a shared file changes?** A change to `shared/base-values.yaml` or the chart itself affects every cluster that uses it, so it should not silently deploy everywhere. Handle it deliberately: the detector does not fan out on shared paths. Instead a *promotion workflow* reads `rings.yaml` and starts the same `fleet-deploy` pipeline ring by ring (canary first, a wait and a health check, then the next ring), usually started by a person or a scheduled release process. Same pipeline, different driver.

**Failure and rollback: Git versus reality.** If the deployment fails and rolls back, Git now says 2.5.0 while the cluster runs 2.4.1. Decide the rule up front: a failed deployment alerts the owner and the commit status shows failure; the owner either fixes forward or reverts the commit (which triggers a deployment of the old version, a no-op if already there). Do not leave the mismatch unattended.

**Drift detection (because Spinnaker does not reconcile).** A scheduled job (nightly) reads each cluster file and compares it with the cluster: the version from the `helm.sh/chart` label on the Deployment, the image tag, the namespace. Differences raise an alert. This catches manual changes and failed deployments that were not followed up.

**Concurrency and ordering.** Two executions for the same cluster must not overlap. The CI job-level concurrency group above serializes them per cluster while still allowing different clusters to deploy in parallel (here up to five at once). Spinnaker's own "disable concurrent executions" setting applies to the whole pipeline, which would make every cluster queue behind the others, so use it only if you want that.

**Security of the trigger.** A webhook endpoint that starts production deployments must not be open. Restrict network access to the CI system's addresses, put authentication in front of Gate, or call the authenticated pipeline-start API (with parameters) instead of an anonymous webhook. Record the commit SHA and the requesting identity on every execution and on the deployed objects (annotations) for audit.

**Guardrails in the repository.** Schema validation of every cluster file in CI; the chart version must exist; accounts must be on an allow-list; CODEOWNERS approvals for production; an optional rule that one pull request may change at most N clusters; and a dry run (render only) of the chart in CI so errors are found before any cluster is touched.

**Why this design works.** Pipeline logic is written once, so a fix or improvement applies to every cluster. Per-cluster differences are data in Git, with review and history. The unit of deployment is one cluster, which gives a small blast radius, and a change to one cluster's file runs the pipeline for that cluster only.

**The interview answer, in two minutes.**

> "I'd keep a fleet configuration repository with one small file per cluster: the Spinnaker account, namespace, chart version, image tag and ring, plus a values file per cluster. There's one common pipeline, `fleet-deploy`, with a webhook trigger. It doesn't know about specific clusters. It validates its input, bakes the Helm chart at the version in the payload with the cluster's layered values, deploys to the account named in the payload, waits for stability, smoke tests, and rolls back on failure. A change detector in CI works out which cluster files changed in a merge and starts one execution per changed cluster, so editing `prod-cell-102.yaml` deploys only cluster 102. I serialize executions per cluster, protect the trigger, alert on failed deployments, and run a nightly drift check, because Spinnaker doesn't reconcile. Shared changes go through a ring-by-ring promotion that uses the same pipeline."

### Other patterns (short)

* **Parameterized pipeline run by hand:** the same pipeline with parameters `cluster` and `version`, started manually or from an orchestrating pipeline. Fine for a few clusters; the operator must supply the right values each time.
* **Generated pipelines from a template:** a pipeline template (managed pipeline templates, or pipeline-as-code such as Dinghy, depending on your distribution) instantiated per cluster. Use it when a stage field such as the target account cannot take an expression, or you want each cluster to have its own pipeline definition generated from one source.
* **Ring orchestration:** a parent pipeline that runs the deployment pipeline for each cluster in a ring in parallel, then verifies and waits before the next ring. Spinnaker has no built-in loop over a list, so the fan-out comes from parallel branches, generated stages, or (as above) from CI.
* **GitOps controllers:** with Argo CD, the same requirement is a different version number in each cluster's folder, and the controller in each cluster applies only its own change.

### Operating Spinnaker: what to get right in practice

* **Idempotence and restart.** If cluster 37 of 100 fails, only that execution fails; fix the cause and restart the failed stage or the execution (stages must be safe to run twice), or roll back only that cluster.
* **Credentials.** Each account is a credential; give each the minimum permissions, and restrict who may run pipelines against production accounts (Spinnaker's authorization).
* **Visibility.** Record the deployed version per cluster (execution history, labels on the objects, and a report built from the repository) so you can answer "which cluster runs which version?"
* **Stability checks.** Use the Deploy stage's wait-for-stable option; otherwise the stage can report success when pods are crash-looping.
* **Safety.** Canary analysis and automatic rollback; manual approval for production rings; fail the pipeline on unexpected diffs.
* **It is a platform to operate.** Many services, a backing store, careful upgrades, and high availability of its own; treat it as production infrastructure.

## 7.5 Argo CD versus Spinnaker in detail

Both deploy software to Kubernetes, but they answer different questions. **Argo CD asks: "does the cluster match what Git says?"** and keeps correcting it until it does. **Spinnaker asks: "how do I safely move this release through a sequence of stages?"** and runs a workflow to do it.

| | **Argo CD** | **Spinnaker** |
| :--- | :--- | :--- |
| Model | Pull-based GitOps: a controller in or near the cluster compares Git with the live cluster and syncs | Push-based orchestration: pipelines of stages push a release to targets |
| Source of truth | Git (manifests, Helm values, Kustomize overlays) | The pipeline definition plus the artifact (image) being deployed |
| Targets | Kubernetes only | Kubernetes, VMs and Auto Scaling groups, ECS, Lambda, several clouds |
| Drift | Detected continuously; can be reverted automatically (self-heal) | Not continuously reconciled; drift persists until the next deploy |
| Release strategies | Sync waves and hooks; canary and blue/green through Argo Rollouts | Built-in rolling, blue/green and canary, automated canary analysis, manual approval gates, parallel branches |
| Many clusters or cells | ApplicationSets generate one application per cluster, environment or cell | Stages deploy to accounts and clusters in a chosen order |
| Credentials | The controller needs rights on the clusters it manages (can run one per cluster) | A central service holds credentials for every target |
| Running it | Fairly light: a few components | Heavy: many microservices (orchestration, cloud driver, API, UI, triggers, metadata, authorization, bake) with a backing store; upgrades take care |
| Learning curve | Gentle for Kubernetes teams | Steeper; pipeline concepts and a large surface area |
| Community | Very active and growing | Mature, but community momentum has appeared to slow as many teams moved to GitOps tools; commercial distributions exist |

**How Argo CD works in practice.** You store manifests (or Helm charts with values) in Git. An *Application* points to a path in a repository and a destination cluster and namespace. The controller renders the manifests, compares them with the live objects, and marks the application *Synced* or *OutOfSync*. With automated sync it applies changes itself; with *prune* it deletes objects removed from Git; with *self-heal* it reverts manual edits. A release is a change in Git: someone updates the image tag in a pull request, review approves it, merge triggers the sync. Promotion across environments is more commits (often automated). Rollback is a revert in Git.

**Argo CD: advantages.**

* **Git is the audit trail.** Every change is reviewed, attributable and reversible with a revert, which suits compliance and incident forensics.
* **Self-healing** removes the class of problems caused by hand-edited production objects.
* **Scales to fleets** with ApplicationSets and gives a clear picture of which cluster is in or out of sync.
* **Lower operational weight,** and works well when each cluster runs its own Argo (a smaller blast radius, and no central system holding every cluster's credentials).
* **Kubernetes-native** concepts, with Helm and Kustomize support.

**Argo CD: drawbacks.**

* **Kubernetes only,** so it does not cover VMs, ECS or Lambda.
* **Release orchestration is thin** by itself: staged rollouts with metric analysis need Argo Rollouts, and approvals or multi-stage promotion need extra tooling or conventions.
* **Fights with other controllers.** An autoscaler changing replica counts or a webhook mutating a field can leave an application perpetually OutOfSync unless you configure ignore rules.
* **Secrets and promotion need design** (external secrets, sealed secrets, a repository layout for environments) because Git is the truth.
* **Eventual, not transactional:** a sync of many resources is not an atomic release with a pass or fail verdict like a pipeline stage.

**How Spinnaker works in practice.** A pipeline is triggered by a new image or a CI job finishing. Stages might be: deploy to a preview environment, run integration tests, run an automated canary analysis that compares metrics of the new version with the old, wait for a manual approval, deploy to the first cell, verify, then deploy to the next group in parallel. If a stage fails, the pipeline stops or rolls back. Kayenta, its canary analysis component, scores the new version statistically against the baseline.

**Spinnaker: advantages.**

* **True release orchestration:** ordered stages, approvals, parallel branches, automated canary judgment, and cross-account and cross-region promotion in one workflow.
* **Heterogeneous targets:** useful when part of the estate is not Kubernetes (VMs or ECS during a migration).
* **Deployment-centered visibility:** what version is running where, and what each pipeline execution did.

**Spinnaker: drawbacks.**

* **Operational heaviness:** many services, a backing store, careful upgrades, and capacity planning of its own; it is a critical platform that needs high availability.
* **Pipelines are less reviewable than Git manifests** unless you template them as code, and pipeline sprawl is a real problem.
* **No continuous reconciliation:** manual changes and drift persist.
* **Central credentials:** a compromise of Spinnaker is a compromise of every target it can deploy to, so permissions need discipline.
* **Community momentum** appears to have slowed compared with the Argo projects, which affects hiring and long-term support decisions.

**How to choose.**

* If everything is Kubernetes and the priority is "every cluster matches Git, with review and self-healing," choose **Argo CD** (add Argo Rollouts for canary).
* If you need **orchestrated, gated, multi-stage releases across heterogeneous targets** with automated canary analysis, **Spinnaker** fits, at the cost of running it.
* Many organizations use **both**: Argo CD to keep cluster state (platform add-ons, configuration) matching Git, and an orchestrator for the staged application rollout across cells; or Argo CD with Argo Rollouts and a promotion tool replacing Spinnaker over time.

**Coexistence pattern in large enterprises.** Legacy or multi-runtime platforms often deploy applications with Spinnaker while adopting Argo CD and GitOps for newer Kubernetes services. A strong interview position: Spinnaker's strength for a cell-based service is staged, gated rollout across many cells with automated canary analysis; Argo CD's strength is keeping each cluster's add-ons and configuration continuously reconciled with Git.

# Part 8: Kubernetes security, secrets and certificates

## 8.1 Kubernetes security architecture (layered)

Think in layers: cloud account, cluster, workload, supply chain, runtime, and people.

| Threat | Controls |
| :--- | :--- |
| Stolen service account token or over-broad RBAC | Least-privilege RBAC, bound short-lived tokens, disable automatic token mounting when not needed, no standing cluster-admin |
| Pod steals node credentials (request forgery to the metadata service) | IMDSv2 with hop limit 1, IRSA or Pod Identity, network policy blocking the metadata address |
| Container escape through a privileged pod | Pod Security Standards at *restricted*, no privileged, hostPath or hostNetwork, non-root, read-only root filesystem, dropped capabilities, seccomp, dedicated nodes for sensitive workloads |
| Malicious or vulnerable image | Scan in ECR and CI, sign images (for example with cosign) and verify at admission, pin by digest, approved registries only, software bill of materials |
| Lateral movement | Default-deny network policies, mesh mutual TLS plus authorization policies, security groups for pods, controlled egress |
| Secret leakage | Envelope encryption with KMS, external secrets, rotation (and a reloader so pods pick up new values), nothing in images or Git |
| API server abuse | Private or restricted endpoint, SSO-based access entries, audit logs shipped and alerted on (exec into pods, reading secrets) |
| CI/CD compromise | Protected branches, signed commits, build provenance, OIDC instead of long-lived keys, least-privilege deploy roles |
| Runtime compromise | GuardDuty EKS runtime monitoring or Falco, immutable nodes (Bottlerocket), no SSH (Session Manager), node and container logging |
| Tenant crossover | Namespaces plus quotas plus policy; dedicated nodes or clusters for sensitive tenants |

**Admission control.** Kyverno, OPA Gatekeeper or the built-in ValidatingAdmissionPolicy block unsafe workloads. Roll new policies out in *audit* mode first, because a strict policy (or a down webhook with a fail-closed setting) can block every deployment.

**Benchmarks and hygiene.** The CIS Kubernetes benchmark (kube-bench), the EKS best-practices guide, regular node image patching through Karpenter drift or managed node group updates, and a patch SLA by severity.

**Air-gapped or regulated/federal clusters.** No internet egress: mirror every container image and Helm chart into a private registry (ECR with VPC endpoints, or an internal registry), verify provenance and signatures offline, bring updates through a controlled transfer process, use internal DNS, time and certificate authorities, vendor charts and dependencies, and meet hardening and cryptography requirements (confirm the specific standards with the team that runs it).

## 8.2 Secrets: External Secrets Operator versus Secrets Store CSI driver

Both bring secrets from a central store (AWS Secrets Manager or Parameter Store) into pods without putting the values in Git, but they work differently, and many platforms (including large-scale multi-tenant data platforms) use both.

**External Secrets Operator (ESO): sync into Kubernetes Secrets.**

* *How it works:* You define a `SecretStore` (or a cluster-wide `ClusterSecretStore`) that says how to reach AWS and with what identity (typically an IAM role via IRSA or Pod Identity), and an `ExternalSecret` that names the secret to fetch, how often to refresh (`refreshInterval`), and the name of the Kubernetes Secret to create. A controller fetches the value and creates or updates a normal Kubernetes Secret, which pods use as environment variables or mounted files.
* *Strengths:* It works with any workload (even charts that expect a Kubernetes Secret, TLS secrets for ingress, image pull secrets); the `ExternalSecret` manifest is safe to keep in Git because it contains no secret value; templating lets you assemble connection strings; many backends are supported.
* *Weaknesses:* The secret value lives in the cluster's datastore as a Kubernetes Secret, so you must encrypt Secrets at rest (KMS envelope encryption) and restrict who can read Secrets; rotation depends on the refresh interval and pods using environment variables need a restart; the operator is a critical dependency; and every `ExternalSecret` polls the AWS API, so thousands of them can cause throttling.
* *Multi-tenancy caution:* a `ClusterSecretStore` lets any namespace request any secret that its IAM role can read. Use namespaced stores with narrowly scoped roles per tenant, and policy to restrict which names a namespace may request.

**Secrets Store CSI driver (with the AWS provider): mount into the pod.**

* *How it works:* A `SecretProviderClass` lists the secrets to fetch. A pod mounts a CSI volume that references it; when the pod starts, the driver (a DaemonSet on every node) fetches the secrets using the pod's own identity and writes them as files into an in-memory volume. Optionally it can also mirror them into a Kubernetes Secret.
* *Strengths:* By default the value is never stored as a Kubernetes Secret, only in the pod's memory-backed volume; access is scoped by the pod's own IAM role, so each workload sees only its secrets; fetching happens at pod start, so the pod's identity decides.
* *Weaknesses:* It is tied to the pod lifecycle (the pod will not start if the secret cannot be fetched, which can be good or bad); the application must read files (not environment variables) and re-read them when the file changes after rotation (the driver can refresh files on an interval); and you need the volume mount in every pod spec.

**Choosing.**

| Need | Use |
| :--- | :--- |
| A chart or component that only accepts a Kubernetes Secret (ingress TLS, image pull, third-party Helm chart) | External Secrets Operator |
| Highly sensitive value that should not sit in the cluster datastore | Secrets Store CSI driver |
| Per-pod identity for least privilege | CSI driver (or ESO with per-namespace stores) |
| Simple Git-friendly declaration across many namespaces | External Secrets Operator |

**Rotation without downtime.** Keep two valid credentials during the rotation window (the old and the new), update the central secret, let ESO or the driver refresh, trigger a rolling restart of pods that read environment variables (a "reloader" watches Secret changes and restarts the workload), confirm health, then retire the old credential. Alert on secrets nearing expiry and on sync failures.

## 8.3 Certificate management in Kubernetes

Certificates appear at several layers, each with its own owner and risk. Naming the layers is the first step of a good answer.

| Layer | What it secures | Who issues and renews | Main risk |
| :--- | :--- | :--- | :--- |
| Control plane and kubelet | API server, kubelets, internal components | On EKS, AWS manages the control plane certificates; kubelet certificates rotate automatically when configured | Rarely yours on EKS; self-managed clusters need rotation processes |
| Edge (load balancer) | Users to the ALB or NLB | AWS Certificate Manager (ACM), renewed automatically when validation records remain in place | Validation record removed, certificate not in use, wrong certificate attached |
| In-cluster application TLS | Pods, ingress controllers, internal services | **cert-manager** | Issuer misconfiguration, DNS challenge permissions, rate limits |
| Mesh (mutual TLS) | Service-to-service identity | The mesh's certificate authority (Istio's istiod), short-lived workload certificates | Root certificate expiry, control plane outage |
| Webhook serving certificates | Admission webhooks called by the API server | cert-manager or the component itself | Expiry blocks all deployments |
| People and automation | Access to the API | Avoid client certificates; use SSO and short-lived tokens | Long-lived credentials |

**cert-manager, explained.** cert-manager is a controller that obtains and renews certificates automatically. You declare an **Issuer** (or cluster-wide **ClusterIssuer**) that says how certificates are obtained, and a **Certificate** that says what you need. cert-manager requests the certificate, stores it (and its private key) in a Kubernetes Secret, and **renews it automatically before it expires** (by default when a third of its lifetime remains), updating the Secret so ingress controllers and pods pick up the new one.

Issuer types: **ACME** (Let's Encrypt or another public CA: proves domain control by an HTTP challenge, or by a DNS challenge that creates a DNS record, for example in Route 53 using an IAM role); **a private CA** (your own CA key stored as a Secret, **Vault**, or **AWS Private CA** through a plugin) for internal certificates; and **self-signed** for bootstrapping.

```yaml
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata: { name: letsencrypt-prod }
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    email: platform@example.com
    privateKeySecretRef: { name: letsencrypt-account-key }
    solvers:
      - dns01:
          route53: { region: us-east-1 }     # uses an IAM role (IRSA) allowed to edit the hosted zone
---
apiVersion: cert-manager.io/v1
kind: Certificate
metadata: { name: orders-tls, namespace: shop }
spec:
  secretName: orders-tls                     # the Secret that will hold tls.crt and tls.key
  duration: 2160h                            # 90 days
  renewBefore: 720h                          # renew 30 days before expiry
  dnsNames: [orders.example.com]
  issuerRef: { name: letsencrypt-prod, kind: ClusterIssuer }
```

You can also annotate an Ingress and let cert-manager create the Certificate for you. **trust-manager** distributes CA bundles to namespaces so pods trust your private CAs.

**On AWS you have two paths for ingress certificates.** Terminate TLS at the ALB with an **ACM** certificate (simplest, managed renewal, the private key never leaves AWS), or terminate in-cluster (ingress controller or mesh gateway) using a cert-manager certificate, which you need when TLS must reach the pod or when you use a private CA. Many platforms use ACM at the edge and the mesh (mutual TLS) or cert-manager inside.

**Istio's certificates.** istiod acts as a certificate authority: each workload receives a short-lived certificate (about 24 hours by default) carrying its identity (a SPIFFE URI built from namespace and service account), delivered to the sidecar and rotated automatically. The sensitive part is the **root of trust**. By default Istio creates a self-signed root that lasts years; in production plug in your own CA (an intermediate signed by your organization's root, often through cert-manager's istio-csr component) and plan the root's expiry and rotation long before it happens, because an expired root breaks every mutual TLS connection at once.

**Operating certificates at scale (for example 100 clusters).**

* **Inventory and monitor expiry everywhere:** cert-manager exposes a metric with each certificate's expiry time (alert at 21 days and 7 days); ACM publishes a days-to-expiry metric; a blackbox probe checks the certificate that clients actually receive (it catches a wrong or stale certificate).
* **Automate renewal and test it,** including the challenge path (the DNS role's permissions, the hosted zone).
* **Watch rate limits** of public CAs when many clusters request the same names; use a private CA for internal names, and separate hostnames per cluster.
* **Protect private keys:** limit who can read the Secrets, encrypt Secrets at rest, rotate on suspicion of exposure.
* **Webhook certificates:** use cert-manager's CA injector so webhooks never expire silently; an expired webhook certificate can block all deployments.
* **Time:** certificate validation depends on accurate clocks; keep time synchronization healthy.
* **Rehearse a root or intermediate CA rotation** in a lower environment; it is the rarest and most dangerous operation.

**Failure modes:** DNS challenge fails because the role cannot edit the zone; ACM validation record deleted; a renewal fails silently and nobody is alerted; the mesh root expires; an ingress still serves an old certificate because the controller did not reload; clock skew makes valid certificates look expired.

## 8.4 A secure software supply chain and deployment platform

**The risk.** An attacker who can change what runs in production controls it. The chain from source code to a running pod has many links, and each can be attacked: a stolen developer credential, a malicious dependency, a compromised build server, a tampered image in the registry, or an unauthorized manual deploy.

**The design, link by link.**

1. **Source:** protected branches, required reviews, signed commits, and dependency scanning. Changes reach production only through reviewed pull requests.
2. **Build:** CI builds the image in an isolated, ephemeral environment. The pipeline authenticates to AWS using **OIDC federation** (the CI system presents a short-lived signed identity token that AWS exchanges for temporary credentials), so there are no long-lived access keys to steal, and the role is limited to pushing to this team's repository.
3. **Scan:** the image and dependencies are scanned for known vulnerabilities; builds fail above a severity threshold, with an exception process.
4. **Describe:** the build generates a **software bill of materials (SBOM)**, a list of every component in the image, and a **provenance attestation**, a signed statement of what source, builder and steps produced it (the SLSA framework defines levels of this).
5. **Sign:** the image is signed (for example with cosign, using a key in a managed key service or keyless signing tied to the CI identity), and the signature is stored beside it in the registry.
6. **Store:** only the private registry holds production images; deployment references an image by **digest** (an exact content hash), not a movable tag.
7. **Admit:** an admission policy (Kyverno, OPA Gatekeeper, or a signature-verification controller) checks every new pod: the image comes from the approved registry, the signature verifies, the digest is pinned, and the pod meets the security settings (non-root, no privilege escalation). Anything else is rejected at the API.
8. **Deploy:** through GitOps, with the cluster's own controller pulling approved changes, so humans and CI do not hold broad cluster credentials.
9. **Detect:** runtime threat detection (GuardDuty EKS runtime monitoring or Falco) and audit alerts on unusual actions (a shell started in a production pod).

**Failure modes and answers.** A compromised CI runner (isolate and limit its permissions, short-lived tokens, builds in clean environments); an emergency need to deploy an unsigned image (an audited break-glass path with time limits); scanner noise (severity thresholds, triage owners, patch SLAs by severity); a policy outage blocking deploys (audit mode first, high availability for the policy engine).

**Measure.** Percentage of running workloads with verified signatures and SBOMs, mean time to patch a critical vulnerability across the fleet, and the number of break-glass uses.

## 8.5 An air-gapped (federal) EKS environment

**What "air-gapped" means here.** The environment has no route to the public internet. Everything the cluster needs must be inside the network or brought in through a controlled process.

**The design.**

* **Network:** a dedicated account and VPC without internet or NAT gateways, with **VPC endpoints** (private connections) for the AWS services needed: the container registry (two endpoints for the API and the Docker protocol), S3 (a gateway endpoint, because image layers come from S3), STS, EC2, logs, secrets and others. The EKS API endpoint is private.
* **Images:** all container images are mirrored into a private registry in the environment (using tools that copy images between registries), scanned, and signed. Nodes pull only from there. No public registries are reachable.
* **Charts and manifests:** Helm charts and their dependencies are vendored (copied) into an internal repository or stored as OCI artifacts in the private registry; GitOps pulls from an internal Git server.
* **Updates:** new versions arrive through a controlled transfer process (for example a reviewed import with signature verification using public keys held inside the environment) and are promoted through environments.
* **Platform services inside:** DNS (private zones), time synchronization, an internal certificate authority, an internal identity provider integration, and logging and monitoring that do not depend on external services.
* **Node images:** built internally from approved sources (Bottlerocket or hardened images), patched through the same controlled process.
* **Access and audit:** strictly limited human access, strong audit logging, session recording, and separate accounts and credentials from other environments.

**Challenges.** Patch latency (every update passes through the transfer process), operators and charts that assume internet access (downloading CRDs or plugins at runtime), applications calling external APIs, and observability or AI tooling that needs outbound access. Confirm the specific compliance requirements with the team that owns the environment; do not claim federal experience you do not have.

# Part 9: Observability, monitoring and incident response

## 9.1 The tools in plain terms

**Three kinds of data.** *Metrics* are numbers over time (cheap, good for dashboards and alerts: "is something wrong, and how bad?"). *Logs* are records of events ("what exactly happened?"). *Traces* follow one request across services ("where did the time go?"). Add *synthetic checks* (robots that really log in from several regions) and *event markers* (deploys, failovers) on graphs.

* **Prometheus.** Pulls (scrapes) metrics from /metrics endpoints and stores them as time series: a name plus labels (service, cell, status). It finds targets through **service discovery** (AWS instance tags, Kubernetes labels), so a new server with the right tag is monitored without registration. Alerts go through **Alertmanager**, which deduplicates, groups, routes and silences. **Cardinality** is the danger: every unique label combination is a separate series, so labels like user ID or request ID can exhaust memory. One Prometheus does not scale to a fleet, so data is sent (remote write) to a scalable long-term store such as **Mimir**, Cortex or Thanos (object storage underneath, per-tenant isolation).
* **PromQL examples:** `rate(http_requests_total[5m])` (requests per second); `sum by (service) (rate(http_requests_total{status=~'5..'}[5m])) / sum by (service) (rate(http_requests_total[5m]))` (error ratio); `histogram_quantile(0.99, sum by (le) (rate(http_request_duration_seconds_bucket[5m])))` (p99 latency).
* **Grafana.** Dashboards and alerting over many data sources (Prometheus or Mimir, Loki, Splunk, CloudWatch). Use variables (cell, service) so one dashboard serves every cell; define dashboards and alerts as code.
* **Loki versus Splunk.** Loki indexes only labels and stores raw logs cheaply (slower ad hoc search, much lower cost). Splunk indexes full content: powerful search, mature security (SIEM) use, higher cost per gigabyte. A common split: security and audit logs in Splunk, high-volume application logs in Loki.
* **Splunk.** Collection by forwarders or the HTTP Event Collector (HEC); **indexers** parse (timestamp, source type) and store data in hot, warm, cold and frozen buckets; **search heads** run searches written in SPL. Cost follows ingest volume or compute, so control it at ingestion (drop noise, sample, short retention for low-value logs, chargeback by team). Search well: narrow by index and time first, filter early, prefer `stats` over `transaction` or `join`, use `tstats` for fast aggregates.

```spl
index=app status>=500 | timechart span=5m count by service
index=app earliest=-1h | stats count as total, count(eval(status>=500)) as errors by service | eval error_rate=round(errors/total*100,2) | sort - error_rate
| tstats latest(_time) as last_seen where index=app by host | eval age_sec=now()-last_seen | where age_sec>600     (hosts that stopped logging)
```

* **Missing logs in Splunk:** work from the source: agent running and queue draining? HEC returning errors? timestamps parsed correctly (events can land in the wrong time range)? routed to the wrong index? quota or license blocking? retention? Reconcile counts at the source and in the index.
* **Datadog.** Commercial all-in-one (metrics, logs, traces, alerts). Quick to adopt; costs grow with hosts, custom metrics and logs.
* **OpenTelemetry.** A vendor-neutral standard: applications emit telemetry using SDKs; a **Collector** adds labels (cell, service), drops noise, samples traces and exports to any backend. Instrument once, change backends freely. Tail sampling keeps all slow or failed traces.
* **CloudWatch.** Source of AWS-managed service metrics (load balancers, RDS, EBS, NAT) and logs; pull into Grafana for one view. Mind the one to two minute delay and the cost of custom metrics. **Kinesis** appears as a pipeline transport (shards; watch iterator age for consumer lag). **CloudTrail, Config and VPC Flow Logs** are the audit and network records.
* **ThousandEyes** runs tests from many places (page loads, DNS, network paths, internet routing) to tell whether a user's failure is your service, their ISP or a routing problem.

**A new cell gets monitored automatically** when the same Terraform module that creates it also creates its collector config, dashboards and default alerts from the cell ID; Prometheus discovers targets by tag or label (pull); log agents baked into the image or deployed per node push to Splunk or Loki; a reconciliation job compares what exists with what is scraped to catch mislabeled resources.

## 9.2 SLOs, burn rate and alert quality

* **SLI** is a measured indicator (percentage of logins that succeed within two seconds); **SLO** is the target (99.9 percent over 30 days); the **error budget** is the allowed failure (0.1 percent); **burn rate** is how fast it is being used. A burn rate of 14.4 for one hour consumes about 2 percent of a 30-day budget.

| Alert | Long window | Short window | Burn rate | Action |
| :--- | :--- | :--- | :--- | :--- |
| Fast burn | 1 hour | 5 minutes | 14.4 | Page now |
| Slow burn | 6 hours | 30 minutes | 6 | Page |
| Trend | 3 days | 6 hours | 1 | Ticket |

The short window makes the alert stop soon after the fix.

* **Availability math:** 99.99 percent is about 52 minutes of downtime a year; 99.999 percent about 5.3 minutes. Serial dependencies multiply (two 99.99 percent parts give about 99.98 percent).
* **SLOs for a login service:** login success rate (excluding user error), authentication latency at p95 and p99, token issuance success, multi-factor delivery success, and admin and provisioning API availability.
* **"You get 100+ alerts an hour. What do you do?"** (1) Triage now: separate page-worthy from noise and suppress duplicates from one cause. (2) In a day or two find the source: alert volume by rule is usually dominated by a few noisy or unowned rules. (3) Structural fix: SLO and burn-rate paging, an owner and runbook for every alert, delete unowned alerts, auto-remediate known transients. (4) Prevent recurrence: track pages per on-call shift and the percentage actionable weekly, and require new alerts to meet a bar.

## 9.3 Incident response

**Mitigate first, diagnose second.** Declare severity; name an incident commander, a technical lead and a communications owner; stabilize with the fastest safe action (roll back, fail over, shift traffic, feature flag); post updates on a regular cadence; keep a timeline; avoid many people changing things at once. Afterward, a blameless review with owners and dates for each action, tracked to closure and fed into the automation backlog. A **security-related** incident also involves Security and Legal immediately, preserves evidence and controls disclosure.

## 9.4 Using generative AI for incident triage

Expect a question like "how would you use AI to speed up triage, and how would you keep it safe?"

**A sensible design.**

1. **Trigger:** an alert fires.
2. **Enrich automatically:** gather context a human would look up: recent deploys and config changes, related alerts, key metrics and logs for the time window, the service owner, dependency health, and the matching runbook.
3. **Ask the model for a structured summary:** what is wrong, likely causes ranked with the evidence for each, suggested next checks, and links. Ground it on retrieved runbooks and history (retrieval) so it cites sources instead of guessing.
4. **Human decides.** The output goes to the on-call engineer in the incident channel. Any action that changes production requires human approval, or runs only from a short list of pre-approved, idempotent, rate-limited runbook actions.
5. **Learn:** record whether the suggestion was right and feed it back.

**Guardrails.** Keep sensitive data out of prompts (redact tokens and personal data) and control where data goes; log every prompt and answer; limit what an agent may call (least privilege); put a human approval step before risky actions; handle failure gracefully so triage still works if the model is down.

**Measure it.** Time to first useful hypothesis, time to mitigate, percentage of suggestions accepted, false-lead rate, toil hours saved, and cost per incident. Test it on past incidents before using it live.

**On AWS.** Amazon Bedrock offers managed access to foundation models with features such as guardrails, knowledge bases for retrieval and agents; verify current capabilities before naming specifics. Your honest position: you understand the architecture and risks, and you would start with low-risk, high-volume work (alert grouping, summaries, runbook lookup) before any automated action.

---

## 9.5 Observability for Kubernetes on AWS

**Layers to monitor.** Control plane (API server latency and errors), nodes (conditions, CPU, memory, disk), workloads (restarts, readiness, replicas), the network (DNS, ingress, mesh), storage (volume usage), autoscaling (pending pods, HPA, Karpenter), and cost.

**The components.** **kube-state-metrics** reports object state (is this deployment's replica count right?). **cAdvisor** (in the kubelet) reports container CPU and memory. **node-exporter** reports machine metrics. **metrics-server** serves `kubectl top` and the autoscaler (it is not a monitoring system). The **Prometheus Operator** (kube-prometheus-stack) manages Prometheus with Kubernetes objects: ServiceMonitor and PodMonitor (what to scrape) and PrometheusRule (alerts). AWS-managed options exist: Amazon Managed Service for Prometheus and Managed Grafana, plus CloudWatch Container Insights.

**Useful diagnostic queries** (use these to investigate, and page on user-facing SLO burn, not on each of them):

```promql
increase(kube_pod_container_status_restarts_total[15m]) > 3                       # restart storms
sum(kube_pod_status_phase{phase="Pending"}) > 0                                    # pods that cannot be scheduled
kube_deployment_status_replicas_unavailable > 0                                    # unavailable replicas
rate(container_cpu_cfs_throttled_periods_total[5m]) / rate(container_cpu_cfs_periods_total[5m]) > 0.25   # CPU throttling
container_memory_working_set_bytes / on(namespace,pod,container) kube_pod_container_resource_limits{resource="memory"} > 0.9   # near OOM
kube_node_status_condition{condition="Ready",status="true"} == 0                   # node not ready
kube_horizontalpodautoscaler_status_current_replicas == kube_horizontalpodautoscaler_spec_max_replicas   # HPA at max
histogram_quantile(0.99, sum by (le, verb) (rate(apiserver_request_duration_seconds_bucket[5m])))        # API latency
kubelet_volume_stats_available_bytes / kubelet_volume_stats_capacity_bytes < 0.1   # volume nearly full
```

**Logs.** A Fluent Bit (or OpenTelemetry Collector) DaemonSet ships container logs with Kubernetes metadata to Loki, Splunk or CloudWatch; use structured logs, control volume, and never log secrets. **Events** (scheduling failures, evictions) should be exported too, since they vanish after an hour. **Control plane and audit logs** go to CloudWatch and are searched for security events.

**Traces and mesh signals.** OpenTelemetry for application traces; the mesh gives request rate, errors and latency per service pair without code changes (the four golden signals).

**Multi-cluster monitoring.** Each cluster runs a light agent (Prometheus in agent mode or an OTel collector) that forwards to a central long-term store (Mimir or Thanos) with external labels such as cluster, region and cell; dashboards use cluster variables; the central rules evaluate fleet-wide alerts; keep each cluster able to alert locally if the central system is unreachable.

**Pitfalls.** High cardinality from short-lived pod names (aggregate by workload, drop unneeded labels, set limits per namespace); alerting on causes instead of symptoms; no owner or runbook per alert; monitoring that shares a failure domain with what it watches; and unmonitored add-ons (CoreDNS, the CNI, the load balancer controller, Karpenter) which are single points of failure for the cluster.

**Cost visibility.** Label workloads by team and service, and use OpenCost or Kubecost to attribute spend; watch over-requested resources, idle nodes and cross-zone traffic.

**Say it like this.** "I monitor Kubernetes in layers: control plane, nodes, workloads, network and cost. I page on user-facing SLO burn and use the lower-level signals to diagnose, I ship every cluster's metrics to a central store labeled by cluster and cell, and I keep the monitoring stack outside the failure domains of the clusters it watches."

### 9.5.1 Getting Kubernetes data into Splunk (and other monitoring tools): how it works

**What must be collected, and from where.**

* **Container logs:** the container runtime writes each container's output to files on the node (under `/var/log/containers` and `/var/log/pods`). A collector running on every node (a DaemonSet) tails those files, adds Kubernetes metadata (namespace, pod, container, labels, node) and forwards them.
* **Kubernetes events:** scheduling failures, evictions, image pull errors, OOM kills. Collected from the API by one cluster-level collector (not per node), because events disappear after about an hour.
* **Metrics:** node and container resource use from the kubelet (including cAdvisor), object state from kube-state-metrics, application metrics from `/metrics` endpoints, and control plane metrics.
* **Traces:** from instrumented applications through OpenTelemetry (or from the mesh).
* **Audit and control plane logs:** on EKS these go to CloudWatch and can be forwarded to Splunk for security analysis.

**The Splunk path: the Splunk OpenTelemetry Collector for Kubernetes.** Splunk's collector is a Helm chart that deploys: an **agent** on each node (log collection, host and kubelet metrics), a **cluster receiver** (cluster-level metrics and events), and optionally a **gateway** (a central aggregation point). It sends logs and events to Splunk Platform through the **HTTP Event Collector (HEC)** (an endpoint plus a token) and sends metrics and traces to Splunk Observability Cloud (or Splunk Platform metrics). It replaces the older Splunk Connect for Kubernetes.

```yaml
# values for the splunk-otel-collector Helm chart (key names vary by chart version; check its reference)
clusterName: prod-us-east-1-cell-101        # becomes a label on all data
splunkPlatform:
  endpoint: https://http-inputs-example.splunkcloud.com:443/services/collector
  index: k8s_prod
  logsEnabled: true
  metricsEnabled: false
  # the HEC token comes from a Kubernetes Secret created by your secrets tooling, never plaintext in Git
agent: { enabled: true }
clusterReceiver: { enabled: true }
```

**Steps to roll it out.**

1. In Splunk, create the **index(es)** (for example one per environment or team) and a **HEC token** restricted to those indexes; check that the HEC endpoint is reachable from the clusters (network path, TLS, allow-lists).
2. Store the token in a secrets manager and deliver it to the cluster with your secrets operator.
3. Install the collector with the Helm chart through GitOps, with the cluster name and index values per cluster.
4. Give the collector the access it needs (read-only RBAC for pods, nodes and events) and resource requests and limits suitable for a node agent, and tolerations so it runs on every node (including tainted pools).
5. **Verify:** search Splunk for the cluster name; check that every node is sending (a search for hosts that stopped reporting, as in section 9.1); compare counts at the source and in Splunk.
6. **Tune:** routing and filtering (below), volume and cost.

**Routing, filtering and enrichment.**

* **Annotations** on a namespace or pod (such as `splunk.com/index` and `splunk.com/sourcetype`) route a workload's logs to a specific index and source type; `splunk.com/exclude` drops noisy workloads.
* **Source types** commonly look like `kube:container:<container name>`; index by team or environment so access control and retention can differ.
* **Multi-line logs** (stack traces) need a line-breaking rule so one exception is one event.
* **Structured (JSON) logs** are parsed so fields are searchable.
* **Filtering and sampling** in the collector (drop health-check logs, debug logs, repeated noise) controls cost, because Splunk is priced by volume or compute.
* **Reliability:** a memory limiter protects the agent; a persistent queue on disk lets logs survive restarts and short outages; HEC should be load-balanced with indexer acknowledgment when delivery guarantees matter; collectors back off when HEC is busy.

**Searching Kubernetes data in Splunk (examples).**

```spl
index=k8s_prod k8s.namespace.name=shop log_level=ERROR | stats count by k8s.pod.name | sort - count
   -> which pods in a namespace log the most errors
index=k8s_events reason=OOMKilling | stats count by k8s.pod.name
   -> pods killed for memory
index=k8s_prod | stats count by k8s.namespace.name | sort - count
   -> which namespaces produce the most log volume (cost)
index=k8s_prod trace_id=abc123 | sort _time
   -> follow one request across services
```

**Other tools, and when to choose them.**

| Tool | How it gets data | Fits when |
| :--- | :--- | :--- |
| Prometheus and Grafana (kube-prometheus-stack) | Scrapes metrics from the cluster; Grafana dashboards and alerts | Metrics and SLO alerting, the standard open-source base; pair with Mimir or Thanos for long-term and fleet storage |
| Loki | A log agent ships logs with labels | Cheap high-volume application logs |
| CloudWatch Container Insights (or the Amazon CloudWatch Observability add-on) | An agent sends metrics and logs to CloudWatch | AWS-native, quick start, per-cluster view; costs and cross-cluster views are limits |
| Datadog | A node agent DaemonSet plus a cluster agent | All-in-one commercial service; costs rise with hosts and custom metrics |
| OpenTelemetry Collector | Receives telemetry and exports to any backend | A vendor-neutral pipeline in front of Splunk, Prometheus or others |

**What to alert on.** Page on user-facing SLO burn. Use platform signals as tickets or diagnostics: pod restarts, pods pending, CPU throttling, memory near limit, node conditions, HPA at maximum, API server latency, volumes nearly full, certificate expiry. Also monitor the monitoring: the collectors' queue sizes and drop rates, ingestion lag, and silent nodes.

**Security and hygiene.** Do not log secrets or personal data (filter at the collector); restrict who can search which indexes; keep the collector's permissions read-only; and keep the HEC token out of Git.

## 9.6 Observability for a fleet of EKS clusters

**The design.** Each cluster runs a light **agent** that scrapes metrics locally (Prometheus in agent mode, or an OpenTelemetry collector) and forwards them with **remote write** to a central long-term store (Mimir or Thanos). Each series carries **external labels** (cluster, region, cell, environment) so you can query one cluster or the whole fleet. Logs go through a node-level agent to Loki or Splunk with the same labels, and traces go through OpenTelemetry. Dashboards use a *cluster* variable, so one dashboard serves all clusters. Alert rules are evaluated in two places: the central ruler for fleet-wide and SLO alerts, and locally in each cluster for critical alerts, so a cluster can still page if its link to the central system is down.

**Decisions.** Keep the monitoring platform outside the failure domain of the clusters it watches (its own account and region, with its own health checks); set cardinality limits per team at ingestion (reject or drop series beyond a quota); choose retention tiers (high resolution for days, downsampled for months); and decide what stays local if the central store is unreachable (buffering on disk in the agent).

**Failure modes.** A metric explosion from a bad label (a limit and an alert on series count), alert noise (SLO burn alerts, owners and runbooks), a central store outage (local alerting and buffering), and unmonitored platform add-ons (the network plugin, DNS, the load balancer controller, the autoscaler are single points of failure for each cluster).

**Onboarding a new cluster automatically.** The same Terraform and GitOps definitions that create the cluster install the agent, dashboards and default alerts using the cluster's labels, and a reconciliation job compares the inventory of clusters with the list of clusters actually sending metrics, alerting on any that are missing.

# Part 10: Kubernetes troubleshooting and performance

## 10.1 Kubernetes troubleshooting by symptom

Start with `kubectl get pods -A`, `kubectl describe pod NAME` (the Events at the bottom explain most problems), `kubectl logs NAME --previous`, and `kubectl get events --sort-by=.lastTimestamp`.

| Symptom | Likely causes | First checks |
| :--- | :--- | :--- |
| Pending | Requests exceed free capacity; taints or selectors; volume in the wrong zone; no free IPs; quota | describe pod events, node capacity, PVC status, subnet free IPs |
| ImagePullBackOff | Wrong tag; registry auth; no route to the registry (NAT or endpoints); rate limits | events, registry permissions, ECR and S3 endpoints |
| CrashLoopBackOff | App error; bad config or secret; failing liveness probe; OOM | `logs --previous`, exit code, recent changes |
| OOMKilled (137) | Limit too low; leak; runtime heap larger than the limit | memory over time, limits |
| Service has errors but pods look fine | No endpoints (selector or readiness); wrong port; unhealthy load balancer targets | endpoints, readiness, target health |
| Node NotReady | kubelet or runtime failure; disk or PID pressure; CNI crashing | node conditions, kubelet and CNI logs |
| Pods evicted | Node memory or ephemeral storage pressure | eviction events, who used the resources |
| 5xx only during deploys | No graceful shutdown; readiness too eager; deregistration delay shorter than shutdown | probes, preStop, grace period |
| Slow or intermittent DNS | CoreDNS load; ndots; conntrack; VPC resolver limit | CoreDNS metrics, node-local cache |
| Stuck Terminating namespace | Finalizers; an unavailable API service | leftover resources, `get apiservices` |
| Drain or upgrade blocked | Strict PodDisruptionBudget; removed APIs | `get pdb`, API deprecation scan |
| Deploys fail with webhook timeouts | An admission webhook is down and its failure policy blocks | webhook configurations, control plane to webhook port, security groups |
| Rolling update stuck | New pods not ready (probe, image, config) | `rollout status`, new pod events; `rollout undo` |
| Connection resets after idle time | Idle timeout in a load balancer, NAT or firewall | enable keep-alives, shorter app timeouts |

## 10.2 Debugging pod performance issues on EKS

"The pod is slow" can mean slow startup, slow responses, slow throughput, or slowness only under load or only on some nodes. The method below narrows the cause quickly. Work top-down and gather evidence before changing anything.

### Step 1: Define the symptom precisely

What is slow (a specific endpoint, all requests, startup, a batch job)? How slow compared with normal, and since when? Is it all pods of the service or some? One node or zone? Did a deploy, config change, traffic increase, autoscaling event or node change coincide? Use the service's latency percentiles (p50, p95, p99) and compare with a baseline. If only some pods are slow, compare slow and fast pods (node, zone, version, size, noisy neighbors).

### Step 2: Locate where the time goes

Use distributed traces (or mesh metrics) to see whether the time is in the service itself or in a dependency (database, cache, another service, DNS, an external API). If the slowness is in the dependency, debug there; if the pod's own work is slow, continue.

### Step 3: Check the pod's resources

**CPU.**
* `kubectl top pod POD --containers` shows current CPU and memory.
* **CPU throttling** is the most common hidden cause. A container with a CPU *limit* is allowed a fixed share of CPU time in each 100-millisecond period; bursty workloads that exceed it are paused until the next period, causing latency spikes even when average CPU looks low. Check the ratio `rate(container_cpu_cfs_throttled_periods_total[5m]) / rate(container_cpu_cfs_periods_total[5m])`; above about 25 percent for a latency-sensitive service is a problem. Fix by raising or removing the CPU limit (keep an accurate request), or adding replicas.
* Multi-threaded runtimes may see more CPUs than the limit allows; configure thread pools and garbage collection threads from the container's allowance.

**Memory.**
* Compare the *working set* with the limit (`container_memory_working_set_bytes`). Near the limit means memory pressure: garbage collection thrash (Java, Go, .NET), page cache eviction, and eventually an out-of-memory kill (exit code 137, `kubectl describe pod` shows `OOMKilled`).
* Memory leaks show as a steady climb; fix in the application or restart on a schedule while you investigate.
* Make sure runtime memory settings match the container limit (for example JVM heap flags as a percentage of the container's memory).

**Disk and I/O.**
* Writing heavily to the container's filesystem or `emptyDir` uses node disk and ephemeral storage and can be slow or evict the pod. Check ephemeral storage use and use a proper volume for heavy I/O.
* For EBS-backed volumes, check IOPS and throughput limits of the volume *and* the instance; look at read and write latency and queue depth. Inside the pod, `iostat -x 1` shows wait times and utilization.

**Network.**
* DNS latency (slow lookups before every request), connection setup cost (TLS handshakes without connection reuse), packet loss and retransmits (`ss -ti` shows per-connection retransmits), connection tracking table pressure, and MTU problems. Cross-zone calls add latency.
* Check mesh sidecar CPU and memory if one is injected: an under-provisioned proxy slows every call.

### Step 4: Check the node and the neighborhood

* **Node pressure and contention:** `kubectl describe node NODE` for conditions and allocated resources; node CPU steal time (the hypervisor taking CPU away; on burstable instance types, exhausted CPU credits); load average versus CPU count; many pods packed on one node competing for memory bandwidth or disk.
* **Noisy neighbors:** other pods on the same node using a lot of CPU, disk or network. Compare per-pod usage on the node. Fix with correct requests, priority classes, anti-affinity, or dedicated node pools.
* **Instance type:** burstable instances throttle; network or EBS bandwidth limits apply per instance size.

### Step 5: Look inside the process

* **Get a shell or a debug container.** `kubectl exec -it POD -- sh` if the image has tools, otherwise an *ephemeral debug container* sharing the pod's process namespace: `kubectl debug -it POD --image=nicolaka/netshoot --target=CONTAINER`.
* **Tools:** `top` or `htop` (which threads), `ps`, `ss -s` and `ss -tan` (connections and states), `iostat`, `vmstat 1` (run queue, swap, I/O wait), `strace -p PID -c` (system calls and where time is spent), `perf` or eBPF tools (profile where CPU goes), `tcpdump` (packets).
* **Application profilers:** Java: thread dumps (`jstack`, `jcmd Thread.print`), garbage collection logs, flight recorder; Go: `pprof`; Python: `py-spy`; Node.js: the built-in profiler. **Flame graphs** show where CPU time is spent. Take thread dumps a few seconds apart to see whether threads are blocked on the same lock, pool or dependency.
* **Application metrics:** thread pool saturation, queue depth, connection pool wait time, garbage collection pauses, cache hit rate, slow queries.

### Step 6: Consider scheduling, startup and scaling

* **Slow startup:** a large image (pull time), init containers, slow dependency checks, readiness probe timings, cold caches or a just-in-time compiler warming up. Look at pod events and timestamps (`kubectl describe pod`), and the time from scheduled to ready.
* **Slow only during scale-out or after deploys:** new pods receive full traffic before they are warm; add readiness that reflects warmth, slow-start on the load balancer, or a gradual ramp.
* **Autoscaling lag:** the HPA reacts to metrics with a delay and nodes take time (see 6.1).

### A quick decision guide

| Symptom | First suspects | Evidence |
| :--- | :--- | :--- |
| High latency, low average CPU | CPU throttling; waiting on a dependency; lock or pool contention | Throttle ratio; traces; thread dumps |
| High CPU | Hot code path; GC; too few replicas; noisy loop | Profiler, flame graph; HPA status |
| Latency grows over hours | Memory leak, connection leak, cache growth | Working set trend; open connections; heap |
| Slow only on some pods | A particular node, zone, or noisy neighbor | Compare per-node metrics; steal time |
| Slow after a deploy | Code change, changed limits, new dependency version | Diff of the release; compare canary and baseline |
| Slow at peak only | Saturation: pools, CPU, database connections; autoscaling lag | Saturation metrics; scaling events |
| Slow disk operations | EBS limits, `emptyDir` on busy node disk | iostat; volume metrics |
| Slow startup | Image pull, init containers, probes, warm-up | Pod event timeline |

**Say it like this.** "I locate where the time goes with traces, then check the pod's CPU throttling, memory, I/O and network, then the node and its neighbors, and only then profile inside the process with thread dumps or a flame graph. I compare slow and fast pods and anything that changed, and I fix the cause, such as the CPU limit, the connection pool or the requests, not the symptom."

---

## 10.3 Kubernetes troubleshooting scenarios

1. **Pods pending in only one availability zone.** A zone-bound volume, a subnet with no free IPs, no capacity of the chosen instance type in that zone, or topology spread constraints that cannot be satisfied. Describe the pod, check subnet free IPs, the volume's zone, and the autoscaler or Karpenter logs.
2. **Karpenter launched nodes but pods are still pending.** The pod's taints and tolerations, node selectors or architecture do not match the new nodes; DaemonSets leave too little room; the node reached its maximum pod count; a missing security group or subnet tag blocked the node from joining. Compare the pod's requirements with the NodePool and read the events on both.
3. **Node count and cost exploded.** Pod requests set far above real use, aggressive minimums, many small pods causing many nodes, a NodePool without limits, or consolidation blocked by PDBs or do-not-disrupt annotations. Right-size requests, set NodePool limits, review disruption settings, and check spot versus on-demand mix.
4. **5xx errors during node consolidation or spot interruptions.** Pods were evicted without enough replicas or readiness protection. Need: multiple replicas spread across nodes and zones, PDBs, graceful shutdown with a pre-stop delay, and enough termination grace time.
5. **Cluster DNS is failing.** CoreDNS pods crash-looping, out of memory or too few for the cluster size; upstream resolver problems; the VPC resolver packet limit on nodes hosting CoreDNS; a network policy blocking DNS. Check CoreDNS logs and metrics, scale replicas with cluster size, add a node-local cache, and spread pods across nodes.
6. **`kubectl` is slow or returns 429 or timeouts.** A controller or script is listing and watching too aggressively, or an admission webhook is slow. Check API server request metrics and flow-control rejections, audit logs for the heaviest clients, and webhook latency. Fix the noisy client and give webhooks tight timeouts.
7. **Mesh: requests fail with 503 and response flag UF or UC.** The proxy cannot reach the upstream or the connection was terminated. Check the destination pods' readiness, mutual TLS mode mismatches, connection pool limits, outlier detection ejecting healthy endpoints, and the sidecar's own health.
8. **Mesh: turning on strict mutual TLS broke some callers.** Clients outside the mesh (including load balancer health checks sent straight to pods) cannot speak mutual TLS. Move namespace by namespace, from permissive to strict, exclude health-check ports where needed, and watch error rates.
9. **Mesh: the application fails at startup but works on retry.** The application starts before its sidecar proxy is ready. Configure the mesh to hold the application until the proxy is ready, or add startup retries.
10. **Mesh: one pod gets all the load from a gRPC client.** Long-lived HTTP/2 connections are pinned to one backend. A mesh or client-side load balancing spreads requests per call instead of per connection.
11. **Helm upgrade is stuck or failed.** Check `helm history` and status (pending-upgrade means an interrupted run), failed hooks, immutable field changes (such as a changed selector), CRD ordering, and release size limits (Helm stores releases in Secrets, which have a size limit). Roll back with `helm rollback` or fix and retry.
12. **Argo CD shows OutOfSync in a loop.** Another controller (an autoscaler changing replica counts, a mutating webhook) rewrites a field Argo manages. Add ignore rules for those fields, check sync waves for ordering, and check whether self-heal and another controller are fighting.
13. **HPA flaps or scales too slowly.** Flapping: tighten the stabilization window and use a better metric. Too slow: metrics lag, node startup is slow (add headroom), or the minimum is too low for the spike. Scale on request rate or queue depth, and pre-scale before known peaks.
14. **High latency with low average CPU.** CPU throttling from limits (check throttled-period ratio), a single hot thread, or noisy neighbors. Raise or remove the limit deliberately, fix requests, and check the node.
15. **Repeated out-of-memory kills.** Distinguish the container hitting its memory limit (exit code 137, container restarts) from the node running out of memory (evictions, kernel OOM). Look at working set over time, leaks, runtime heap settings versus the limit, and QoS class (BestEffort pods die first).
16. **Image pulls fail after moving workloads to private subnets or an air-gapped network.** Missing VPC endpoints for the registry and S3, no pull permission on the node role, no pull secret for a private registry, or registry rate limits. Add endpoints, a private mirror or pull-through cache, and verify permissions.
17. **Scale-out causes an image pull storm.** Many new nodes pull a large image at once and hit registry throttling or slow startup. Use smaller images, pre-pulled or cached images in the node image, a regional cache, and staged scale-out.
18. **EFS or EBS volumes will not mount.** EFS: security group must allow NFS (port 2049) from the nodes to the mount targets, mount targets must exist in each zone, and the CSI driver needs permissions. EBS: wrong zone, attachment limit per instance, or a leftover attachment (see AWS scenario 8).
19. **ALB targets for pods are unhealthy, though the pods are fine.** The pod's (or node's) security group does not allow the load balancer's group, the health check path or port is wrong, or strict mutual TLS blocks the health check. Compare the health check settings with the pod's actual listener and check the target reason code.
20. **A secret was rotated and some pods broke.** Pods read the old value (environment variables do not refresh; mounted files can). Use a reloader or rolling restart on change, an external secrets operator with a sensible refresh interval, and dual-valid credentials during rotation.
21. **A new admission policy blocked all deployments.** The webhook is fail-closed and down, or the rule is too strict. Roll policies out in audit mode, give webhooks redundancy and short timeouts, and have a break-glass procedure to disable the policy.
22. **A cluster upgrade broke workloads.** Removed APIs, add-on incompatibility (CNI, CoreDNS, kube-proxy, CSI), or a strict PDB left things half-drained. The control plane cannot be downgraded, so the rollback is to replace nodes with the previous version, fix the add-ons, or shift traffic to a blue/green cluster. Prevent with pre-checks and canary clusters.
23. **One team's batch job starves other teams.** No quotas or priorities. Add resource quotas, limit ranges, priority classes, separate node pools for batch work, and PDBs and requests for critical services.
24. **Pods stay Pending with "too many pods".** The node reached its maximum pod count (limited by network cards and addresses). Use prefix delegation, larger instance types or more nodes, and avoid many tiny pods on small nodes.

# Part 11: Databases and Redis

## 11.1 "The database is slow": a method

1. **Is it the database?** Compare application and database timings; many cases are pool waits, DNS or network.
2. **Scope it:** all queries or a few, one tenant or all, since when, what changed.
3. **Resource picture:** CPU, memory, IOPS and latency, connections, replication lag (RDS: CloudWatch metrics and Enhanced Monitoring).
4. **Find the expensive queries:** Performance Insights (database load by SQL statement and wait type), the slow query log, `SHOW FULL PROCESSLIST`.
5. **Classify:** too much work (missing index), disk waits (storage limits, cold buffer pool), lock waits, connection exhaustion, replication lag.
6. **Stop the bleeding first** (throttle or kill the offender), then fix properly.

## 11.2 The ideas to explain

* **Indexes** work like a book's index: without one the database scans every row. Composite indexes work left to right. `EXPLAIN` shows the plan: look for a full scan (`ALL`), the chosen key, rows examined, and `Using filesort` or `Using temporary`. Stale statistics (`ANALYZE TABLE`) and plan changes after upgrades cause sudden slowdowns.
* **Buffer pool:** InnoDB caches data pages in memory; if the working set exceeds it, performance falls off a cliff, and a failover or restart starts with a cold cache.
* **Locks:** a long-open transaction holds locks and keeps old row versions, slowing everything. Schema changes need a metadata lock that waits for running transactions and blocks new queries behind it, so check for long transactions first and use a short lock timeout.
* **Connections:** each uses memory; pools across many app instances can exceed the limit; RDS Proxy multiplexes connections and survives failovers. A small slowdown can fill pools and become an outage.
* **Replication:** the primary writes a binary log; replicas replay it, asynchronously by default (replicas lag; a failover can lose the last writes). Lag comes from large transactions, slow replica storage, long queries on the replica and serial replay. Break bulk work into batches, enable parallel replay, size replicas like the primary.

## 11.3 Zero-downtime upgrades and schema changes

On one writable database, "zero downtime" means seconds of interruption hidden by retries.

* **Major version on RDS:** use **Blue/Green**. RDS builds a synchronized copy (green), you upgrade it and test, then switch over: writes pause briefly, endpoints swap, applications reconnect to the same name, typically under a minute. An in-place upgrade on Multi-AZ takes the database down for the duration.
* **Minor version:** Multi-AZ upgrades the standby, fails over, then upgrades the old primary (about a minute of failover).
* **Schema changes:** a plain `ALTER TABLE` can lock a large table for minutes. Use an online tool (`gh-ost` or `pt-online-schema-change`: creates a shadow table, copies in chunks, replays changes, swaps atomically) and the **expand-and-contract** pattern so old and new code both work during deploys: add the new column, write to both and backfill, read from the new, drop the old. Never do a destructive schema change and a code deploy in the same step.

## 11.4 Monolith, partitioning or sharding

| Approach | What it is | When to choose |
| :--- | :--- | :--- |
| **Vertical scaling + read replicas + cache** | Bigger instance, replicas for reads, Redis for hot data | Always first; simplest and goes far |
| **Table partitioning** | One table split into physical pieces on the same server (for example by date) | Huge tables where old data is dropped or queries always filter on the partition key; does not scale writes beyond one machine |
| **Cell-based isolation** | Many independent databases, each holding a subset of tenants (each cell has its own database) | Multi-tenant SaaS: strong fault isolation and independent growth without application-level shard routing |
| **Application sharding** | Data split across servers by a shard key in the application or proxy | Only when one logical database outgrows the largest single server; cross-shard queries, rebalancing and schema changes across shards are expensive |

## 11.5 Redis

* **What it does:** single-threaded in-memory data store; fast because data is in RAM and there is no lock contention. Slowness comes from big keys (`DEL` on a huge hash blocks the thread; use `UNLINK`), `KEYS *` in production (use `SCAN`), slow Lua scripts, or network latency.
* **Persistence:** RDB snapshots and AOF append logs; for a pure cache, turn persistence off and avoid disk spikes.
* **Eviction:** `allkeys-lru` or `allkeys-lfu` for caches; `noeviction` when data must not be dropped (rate-limit counters, sessions).
* **Scaling and HA:** Replication Group (primary plus replicas with automatic failover) for most uses; Cluster Mode (16,384 hash slots across shards) when memory or write throughput exceeds one node. Use TLS and authentication in transit.
* **Failure modes to handle in code:** *cache stampede* (many requests rebuild an expired key at once: jitter TTLs, lock); *penetration* (misses for nonexistent keys hit the database: cache negative results); *avalanche* (many keys expire together: stagger TTLs); and *fail open or closed* (if Redis dies, should login fail or fall back carefully to the database?).

# Part 12: System design and reliability

## 12.1 Reliability and design essentials (cells, DR, deployments, resilience)

* **Cell architecture:** an independent copy of the whole stack serving a slice of tenants; an edge router maps each tenant to a cell. Limits blast radius, avoids noisy neighbors, lets you upgrade one cell at a time, and scales horizontally without sharding one giant database. Hard parts: routing consistency, moving a tenant between cells, shared global control data, and keeping every cell identical through automation.
* **Disaster recovery:** **RPO** is how much data you can lose (driven by replication lag); **RTO** is how long recovery takes (driven by failover and verification). Patterns from cheapest/slowest to fastest/costliest: backup and restore, pilot light (data replicating, compute minimal), warm standby (scaled-down copy ready to scale up), active-active. Rehearse failovers regularly; untested DR is wishful thinking. A **delayed replica** protects against human error and bad deploys, because an immediate replica copies the mistake too.
* **Deployments:** rolling, blue/green (two copies, switch traffic, instant rollback), canary (small share of traffic, automated metric comparison, promote or roll back), feature flags (decouple deploy from release).
* **Resilience patterns:** timeouts on every call, retries with exponential backoff and jitter plus a **retry budget** (so retries do not cause a storm), circuit breakers (fail fast when a dependency is broken), bulkheads (separate pools so one slow dependency does not starve others), load shedding (reject excess work early), graceful degradation, idempotency keys, and rate limiting.

## 12.2 A multi-tenant EKS platform for 100+ product teams

* **Requirements:** 100+ teams, thousands of services, mixed workloads (APIs, batch, data tools), strong isolation between teams, fast self-service onboarding, compliance and auditability, predictable cost, and a small platform team.
* **Design:** Cluster boundaries (shared clusters per region and environment for standard workloads; dedicated clusters for regulated or very large tenants, and cell-aligned clusters where the product is cellular). Tenancy inside a shared cluster: a **namespace per team or service**, generated from a template with ResourceQuota, LimitRange, RBAC mapped from SSO, Pod Security Standards at *restricted*, default-deny NetworkPolicy, PriorityClasses, and cost labels. Compute: Karpenter with separate NodePools (general on-demand, spot for batch with taints, dedicated pools where needed) and headroom pods for spiky tiers. Golden path: platform-provided Helm charts and Terraform modules, GitOps with Argo CD ApplicationSets, secrets from AWS Secrets Manager via External Secrets Operator, IRSA or Pod Identity per service, shared ingress gateway and mesh (Istio) for mutual TLS and service-pair metrics, central Prometheus/Mimir, Loki/Splunk, Grafana and OpenTelemetry.
* **Trade-offs:** Shared clusters save money and operational effort, at the cost of noisy neighbors and shared blast radius (mitigated with quotas, priorities, node pools and admission policies). Golden charts speed up 90 percent of teams, with controlled escape hatches for the rest.
* **Failure modes:** Admission webhook outage blocking all deploys (audit mode first, HA webhooks, short timeouts, fail-open for non-critical checks); one team exhausting IPs or API rate limits (quotas, generous VPC CIDRs with prefix delegation, API priority and fairness); a bad add-on upgrade breaking everyone (canary clusters and rings).
* **Rollout and measures:** Build the platform foundation, onboard a friendly pilot team, refine the golden chart, publish self-service onboarding, deprecate legacy paths. Measure time from new service to production, platform availability, percentage of workloads on the golden path, policy compliance, and cost per workload.

## 12.3 A multi-region platform for a login service (99.99 percent or better)

* **Requirements:** 99.99 percent availability (about 52 minutes a year), low p99 latency worldwide, survives a full region loss, handles morning login spikes and credential-stuffing attacks, strong security and auditability.
* **Design:** **Cell-based architecture** across two or more regions. Each cell holds its own stateless login tier (EKS across three zones), Redis cache and rate-limit store, and primary relational database (Multi-AZ), with an asynchronous read replica in a paired region (plus a delayed replica for recovery from bad writes). Edge: Route 53 latency routing or Global Accelerator for health-based steering, CloudFront and WAF (rate limits, bot and account-takeover rules) at the edge, ALB in IP mode to pods. A lightweight, globally replicated routing directory maps each tenant to its home cell.
* **Trade-offs:** Single-writer per cell in one home region avoids multi-master database conflicts and gives strong consistency for credentials, at the cost of a deliberate regional failover (minutes) if a whole region is lost, rather than instant active-active writes. Cells cost more in baseline infrastructure than one giant cluster, which is paid back in blast radius and upgrade safety.
* **Failure modes:** Credential stuffing or retry storm (WAF rate limits at the edge, load shedding, Redis counters, circuit breakers, retry budgets); morning login spike (scheduled pre-scaling, HPA on request rate, Karpenter with headroom pods, connection pooling via RDS Proxy so pod scale-out does not exhaust database connections); database or region failure (Multi-AZ automatic failover inside the cell; for region loss, health checks stop routing to the failed region, promote the cross-region replica, update the tenant directory, and rehearse quarterly so RTO and RPO are proven).
* **Security, observability, cost:** Least-privilege IAM per service, encrypted data and secrets, audit logs; synthetic login probes from global locations, SLO burn-rate alerts, traces and deploy markers; Graviton instances, right-sized requests, spot only for non-critical background work.

## 12.4 Migrating an existing ECS service to EKS

* **Requirements:** Zero user-visible downtime, instant rollback at every step, parity in security, observability and scaling, minimal disruption to the product team.
* **Approach:**
  1. **Assess:** dependencies, traffic patterns, state (ensure sessions and files are externalized), secrets, IAM permissions, compliance needs, current p95 and p99 latency and error rates.
  2. **Prepare EKS:** namespace, IRSA or Pod Identity matching the ECS task role, secrets synced from the same Secrets Manager entries, network connectivity (security groups to the same database and Redis), golden Helm chart, dashboards and alerts.
  3. **Shadow or dark launch:** deploy to EKS with no live user traffic; run synthetic and load tests, verify logs, metrics, traces and scaling.
  4. **Weighted traffic shift:** put an ALB or Route 53 weighted routing in front of both ECS and EKS target groups. Shift traffic gradually: 1 percent, 5 percent, 25 percent, 50 percent, 100 percent, holding at each step to compare latency, error rate and database connections.
  5. **Rollback:** shift weight back to 100 percent ECS at any sign of trouble (keep ECS running warm until EKS has held 100 percent through a peak cycle).
  6. **Decommission:** scale down and remove ECS resources and update runbooks and alerts.
* **Pitfalls:** Connection pool multiplication when both ECS and EKS run at once (adjust pool sizes during the split); DNS caching delaying weight shifts (use ALB target group weights where possible); subtle differences in timeouts, headers or environment variables; missing security group rules to downstream databases.

## 12.5 Upgrading 100 clusters with no downtime

* **Requirements:** Keep every cluster within supported Kubernetes versions (no more than one minor version behind), zero downtime for tenant workloads, safe rollback, predictable schedule.
* **Design:**
  1. **Prepare:** scan every cluster for deprecated or removed APIs (for example with pluto or kubent) and block upgrades on findings; verify the compatibility matrix of EKS version, CNI, CoreDNS, kube-proxy, CSI drivers, load balancer controller, Karpenter and Istio; verify every critical service has multiple replicas, topology spread and a sensible PodDisruptionBudget.
  2. **Ring-based rollout:** group clusters into rings: Ring 0 (internal and staging, 2 clusters), Ring 1 (canary production cells, 3 clusters), Ring 2 (early production, 15 clusters), Ring 3 (general production, 60 clusters), Ring 4 (highest-sensitivity or federal cells, 20 clusters).
  3. **Per-cluster sequence:** upgrade the control plane, then upgrade add-ons in order, then roll the data plane (Karpenter drift or managed node group rolling update, respecting PDBs and draining gracefully).
  4. **Automated health gates between rings:** watch SLO burn rate, API latency, pod restarts, node readiness and DNS error rate for a soak window; pause automatically if any gate trips.
  5. **Rollback:** EKS control planes cannot be downgraded; if a workload breaks, roll back the node group or add-on version, or for high-risk major changes build a blue/green cluster and shift traffic.
* **Measure:** Fleet version compliance percentage, time to roll out across all rings, and number of customer-facing incidents during upgrades (target: zero).

## 12.6 Surviving the loss of an availability zone

* **Requirements:** Continue serving within SLO when one availability zone is impaired or isolated, with no manual emergency surgery.
* **Design:** Spread nodes and pod replicas evenly across at least three zones (`topologySpreadConstraints` with `maxSkew: 1`), run below roughly two-thirds capacity so the remaining two zones absorb the load without waiting for scale-out, use Multi-AZ databases with automatic failover, keep NAT gateways and VPC endpoints per zone (no cross-zone NAT dependency), use topology-aware routing so normal traffic stays in-zone, and configure load balancers to remove unhealthy zone targets (and use zonal shift where supported).
* **Failure modes:** Zone-bound EBS volumes stranding stateful pods (keep stateful data in Multi-AZ managed services, or replicate across zones); asymmetric "gray" failures where a zone is degraded rather than completely down (active health checks and zonal shift); autoscaling trying to launch into the impaired zone (multi-zone node pools and Karpenter handling capacity errors).
* **Validate:** Regular game-day tests simulating a zone evacuation and measuring time to recover and error budget impact.

## 12.7 Disaster recovery for Kubernetes workloads

* **Clarify:** Separate *stateless* clusters from *stateful* data, and state the RTO and RPO targets.
* **Design:** Treat clusters as rebuildable from code: Terraform recreates the VPC, EKS cluster and IAM roles; GitOps (Argo CD) deploys every add-on and application from Git; secrets live in a replicated secrets manager; images live in a multi-region replicated registry. Back up anything not in Git (persistent volumes and runtime cluster state) on a schedule with **Velero** to cross-region object storage, alongside automated database backups and cross-region replicas (including a delayed replica for logical corruption).
* **Cutover:** In the recovery region, stand up or scale up the cluster, verify data replication and promotion, run smoke tests, switch DNS or Global Accelerator, and monitor SLOs.
* **Validate:** Quarterly DR drills that actually restore from backups into a clean cluster and measure real RTO and RPO against targets.

# Part 13: Kubernetes in a networking solution (Nokia EDA)

Nokia Event Driven Automation (EDA) is a modern network automation platform for data center and cloud networks (SR Linux and others) built on Kubernetes, using Kubernetes's declarative APIs, controllers and CustomResourceDefinitions to manage network fabric intent, state and operations. Use this if you work on or interview for a Kubernetes-based networking automation platform (such as Nokia EDA), and adapt the details to what you know directly.

## 13.1 Why Kubernetes suits a network automation platform

A network controller reconciles *intended* network state (VLANs, VRFs, BGP peers, ACLs, interfaces, policies) against *actual* switch and router state, continuously, at scale, with auditability and role-based access. That is the exact problem Kubernetes's control loop was built to solve: CustomResourceDefinitions model network intent as typed API objects, controllers watch for changes and converge devices toward desired state, etcd stores the desired state with optimistic concurrency, RBAC and namespaces provide multi-tenant access control, and Helm and GitOps package and deliver network configurations.

## 13.2 A reference architecture on Kubernetes

* **Control and intent layer:** API server + etcd (or an extension API server) holding network intent CRDs (topologies, fabrics, interfaces, routing policies, tenants), validated by admission webhooks before bad network changes are accepted.
* **Reconciliation and orchestration controllers:** Kubernetes controllers (operators) translate high-level intent into device-specific configuration, compute diffs, order changes safely (for example drain a spine before modifying it), and write status conditions back to the custom resources.
* **Southbound device drivers / adapters:** components that speak gNMI, NETCONF, gRPC or SSH to switches and routers, stream telemetry back, and maintain device sessions. Keep these stateless where possible and shard devices across replicas (consistent hashing or lease-based leader election) so one instance does not hold every session.
* **State, telemetry and event pipeline:** time-series store (Prometheus/Mimir) for interface counters, BGP session states and optic levels; event bus or streaming pipeline for link-down and alarm events; GitOps repository storing network intent as code.
* **Northbound interfaces:** REST/gRPC APIs, web UI, CLI, and Terraform or Ansible integrations so cloud and network teams consume the same platform.

## 13.3 Operating it

* **High availability:** run across three zones; multiple replicas for stateless APIs and workers; leader election for single-active controllers; PodDisruptionBudgets so maintenance never drops quorum; spread southbound workers so a node failure drops only a fraction of device sessions, which reconnect automatically.
* **Safe rollout of network intent (the highest-stakes operation):** validate syntax and topology invariants in admission webhooks; support dry-run / diff preview; roll changes in waves (canary leaf or rack first, verify BGP and traffic counters, then proceed); automatic rollback on health-check failure; approval gates for core fabric changes.
* **Scale and performance:** watch API server and etcd load when thousands of interfaces update status frequently (separate high-frequency telemetry from Kubernetes status objects; put counters in a time-series database, not in etcd); tune controller work queues, rate limiters and resync intervals.
* **Upgrades:** separate platform upgrades (Kubernetes and EDA components) from device OS upgrades; keep southbound protocols backward compatible during rolling upgrades.
* **Security:** least-privilege RBAC per network domain or tenant, mutual TLS between platform services and to devices where supported, device credentials in a secrets manager (never in CRDs), full audit log of who changed which network intent and when.

## 13.4 Failure modes to know

* **Southbound storm:** a fiber cut flaps hundreds of interfaces at once, flooding telemetry and triggering mass reconciliations. Mitigate with rate limiting, event debouncing, backpressure on work queues, and keeping high-frequency state out of etcd.
* **Split brain or duplicate device writers:** two controller replicas push conflicting configs to the same switch. Prevent with leases/leader election per shard and optimistic concurrency (resource versions) on the device.
* **Bad intent pushed fabric-wide:** a typo in a BGP policy isolates racks. Prevent with admission validation, dry-run diffs, canary-rack rollout and automatic rollback on session loss.
* **Platform cluster degraded while the network is still forwarding:** design the data plane (switches) to keep forwarding traffic normally if the management cluster is temporarily down (fail-static management), and host the management cluster on out-of-band management networking so a fabric issue does not cut the controller off from the switches.

## 13.5 A worked example you can adapt for an interview

Adapt this to the specific product or project you worked on, keeping the structure: context, design, trade-offs, failure modes, results.

> **Context.** "We were running a Kubernetes-based network automation platform managing leaf-spine fabrics, where network engineers expressed intent—tenants, VRFs, BGP policies, interfaces—as Kubernetes custom resources, and controllers reconciled that intent onto switches over gNMI."
>
> **Architecture.** "We ran the platform on a multi-AZ Kubernetes cluster on out-of-band management networking so a fabric event could never isolate the control plane from the switches. Intent lived in Git and was applied through GitOps. Admission webhooks validated topology rules before any object hit etcd. Reconcilers computed config diffs and pushed changes through sharded southbound gNMI workers, while high-frequency interface counters went straight to Prometheus rather than etcd so status updates would not overload the API server."
>
> **Safe rollout and resilience.** "Every fabric change ran in dry-run diff mode in pull requests, then rolled out in rings—a canary leaf pair first, checking BGP session health and packet drops before continuing, with automatic rollback if sessions dropped. Southbound workers used lease-based sharding so losing a node only reconnected a slice of devices."
>
> **Trade-offs and lessons.** "The biggest lesson was keeping noisy telemetry out of Kubernetes custom resource status fields and debouncing link-flap storms, which cut API server load dramatically and kept reconciliations predictable under failure."

## 13.6 Questions you may get about this example, with answers

* **Why not just run Ansible playbooks against the switches?** Playbooks are push-based and point-in-time: they do not continuously detect drift, reconcile after a switch reboots, or expose typed APIs with admission validation and RBAC. Kubernetes controllers give continuous reconciliation and a single source of truth; we still integrate with Ansible or Terraform at the edges when teams want to trigger workflows.
* **What happens if the Kubernetes cluster goes down completely?** The switches continue forwarding traffic on their last programmed state—the management plane is out of the packet-forwarding path. While the cluster is down you lose new changes and telemetry, so we run the platform across three zones, back up etcd and Git intent, and keep the management network separate from the data fabric.
* **How do you prevent a bad BGP or ACL change from taking down the whole fabric?** Four gates: schema and topology validation in admission webhooks, a rendered device diff in pull-request review, ring rollout starting with a single canary rack, and automated health checks on BGP neighbors and error counters that trigger rollback before the next ring starts.
* **Why keep telemetry out of etcd?** etcd is designed for small, low-churn desired-state objects, not high-frequency counters from thousands of ports. Writing frequent status updates bloats etcd, triggers watch storms across controllers, and slows the API server. Desired state and coarse health conditions live in CRDs; high-rate counters go to Prometheus.
* **How do you handle a switch that was edited manually on its CLI?** The southbound session detects state drift against the desired intent in the cluster and either alerts (in audit mode) or reconciles it back (in enforce mode), while audit logs record the drift event.

## 13.7 If you meant event-driven architecture (the general pattern)

If "EDA" in the conversation means general **event-driven architecture** on Kubernetes and AWS: producers emit immutable events to a durable broker (Kafka/MSK, EventBridge, SQS/SNS); consumers process asynchronously and scale on queue depth or consumer lag with **KEDA**; every consumer is **idempotent** (using an event ID and deduplication store) because delivery is at-least-once; poison messages go to a **dead-letter queue** with alerts and replay tooling; schemas are versioned for backward compatibility; and end-to-end tracing propagates correlation IDs across async hops.

# Part 14: Linux, coding and scripting

## 14.1 Linux essentials

* **Load average:** runnable tasks plus tasks waiting on uninterruptible I/O (usually disk). High load with low CPU points to disk I/O.
* **Processes:** zombie (finished, waiting for parent to read exit status; uses a table slot, not memory); orphan (parent died, adopted by PID 1). Signals: SIGTERM (15, polite stop) versus SIGKILL (9, immediate, cannot be caught).
* **Memory:** `free -h`: **available** is what matters (free plus reclaimable cache). Linux uses free RAM as page cache, which is healthy. Swap thrashing hurts latency.
* **Disk:** `df -h` (space) versus `df -i` (inodes; many small files exhaust inodes before bytes). A deleted file still held open by a process keeps its space until the process closes it (`lsof +L1`).
* **Troubleshooting order:** `uptime`, `dmesg -T | tail` (OOM killer, hardware errors), `vmstat 1` (run queue, swap, iowait), `mpstat -P ALL 1` (single-core bottleneck), `pidstat 1`, `iostat -xz 1` (await, %util), `free -h`, `ss -s` and `ss -ltnp`, `df -h` and `df -i`.
* **Filesystems and containers:** containers are processes isolated with Linux **namespaces** (PID, network, mount, UTS, IPC, user) and capped with **cgroups** (CPU, memory). OverlayFS layers read-only image layers under a writable container layer.

## 14.2 Coding and scripting tasks for SRE and DevOps interviews

* **Good habits:** set `set -euo pipefail` in bash; stream large files instead of reading all into memory; handle retries with exponential backoff and jitter; use timeouts on every network call; parse JSON with `jq` or Python rather than regex; make scripts idempotent.
* **Common tasks:** parse a web or proxy log and print the top endpoints and 5xx error rates; query an AWS API with pagination and output resources missing required tags; drain or check Kubernetes nodes via the API; poll an endpoint with backoff and exit non-zero on failure; clean up old snapshots older than N days with a dry-run flag.

```python
# Example: paginate EC2 instances missing an "Owner" tag
import boto3

ec2 = boto3.client("ec2")
paginator = ec2.get_paginator("describe_instances")
for page in paginator.paginate():
    for res in page["Reservations"]:
        for inst in res["Instances"]:
            tags = {t["Key"]: t["Value"] for t in inst.get("Tags", [])}
            if "Owner" not in tags:
                print(inst["InstanceId"], inst["State"]["Name"])
```

# Part 15: Interview preparation: interviewer scenarios, short answers, questions and checklists

## 15.1 Scenario questions for platform and SRE architect rounds

Use these to practice thinking out loud. Each has a solid structure: clarify, decide, trade-offs, failure modes, rollout.

* **A single cell's primary database is approaching its vertical limit.** *Structure:* verify queries and indexes first; offload reads to replicas and Redis; archive or partition old data; if truly at the ceiling, split the cell's largest tenants into a new cell (tenant migration with dual-write or short cutover) rather than sharding the database inside one cell.
* **You inherit 40 EKS clusters created by different teams, with different versions, add-ons and security settings.** *Structure:* inventory first (versions, add-ons, policies, owners); define the standard baseline; bring clusters under GitOps management; apply admission policies in audit mode to measure gaps; standardize add-ons and upgrades in rings, starting with non-production; provide a migration guide and office hours.
* **A new compliance requirement demands that all service-to-service traffic in production be encrypted and authenticated within two quarters.** *Structure:* compare mesh mutual TLS (Istio) against CNI encryption (Cilium) and application TLS; choose mesh if identity-based authorization and telemetry are also wanted; deploy the control plane, onboard namespaces in permissive mode, verify health checks and non-mesh callers, switch to strict mode ring by ring, and monitor certificate expiry and latency overhead.
* **Deployments take 45 minutes and fail 15 percent of the time, so teams batch changes into risky weekly releases.** *Structure:* measure where the 45 minutes go (build, tests, image pull, rollout, manual gates); parallelize tests, shrink images, automate canary analysis, replace manual gates with automated SLO checks, enforce graceful shutdown and probes so rollouts do not fail falsely, and track deployment frequency, lead time and change failure rate.
* **Cloud spend rose 35 percent in a quarter while traffic grew 10 percent.** *Structure:* break down by service, account and team (Cost Explorer and OpenCost); check top drivers (over-requested pods, idle nodes, NAT gateway and cross-zone data transfer, log and metric cardinality, unattached volumes and snapshots); fix quick wins (VPC endpoints, lifecycle rules, right-sizing), put Karpenter consolidation and quotas in place, and institute monthly team cost reviews.
* **An internal developer portal wants to offer "one-click new service" on your EKS platform.** *Structure:* generate a repository from a golden template (application skeleton, Dockerfile, golden Helm chart values, Argo CD Application, Terraform for IAM role and secrets, default dashboard and SLO alerts); enforce standards through the chart and admission policy; keep ownership with the service team from day one.
* **How do you measure whether your platform team is succeeding?** *Structure:* developer velocity (time from new service to first production deploy, deployment lead time), reliability (platform availability, SLO attainment across onboarded services, change failure rate), adoption (percentage of workloads on golden charts and standard pipelines, NPS or developer survey), and efficiency (cost per service or request, toil hours reduced).

## 15.2 Six short answers

1. **Tell me about yourself (60 seconds).** "I am a platform and SRE leader focused on running multi-region, high-availability cloud infrastructure on AWS and Kubernetes. Most recently I led SRE across edge networking, EKS platforms, CI/CD, observability and automation for a cell-based identity service at 99.99 percent availability, including multi-cloud and federal environments. I care about turning operational knowledge into paved roads—Terraform modules, golden Helm charts, GitOps, SLO-driven alerting and automation—so product teams ship fast without sacrificing reliability or security. I am excited about this role because of the scale and the chance to build a cohesive Kubernetes platform."
2. **Tell me about a major outage you led.** Use context, impact, action, outcome: calm command, fastest safe mitigation first (rollback or traffic shift), clear communication, blameless review, and concrete prevention shipped afterwards (such as automated canary rollback or a delayed replica).
3. **A time you pushed back on a feature or deadline for reliability.** Explain the risk in user and business terms (error budget, blast radius), offer a safer path (canary, feature flag, phased rollout), and show the result.
4. **How you work with product teams.** Paved roads, not gates: make the safe thing the easy thing (golden charts, self-service onboarding, clear SLOs), embed during big launches, and use error budgets to align on when to slow down for reliability.
5. **Why Terraform over CloudFormation, or vice versa.** Multi-cloud and unified tooling across AWS, Kubernetes and observability favor Terraform; AWS-only with managed rollback favors CloudFormation. Choose for the organization's footprint.
6. **How you keep your skills current.** Hands-on labs, reading postmortems and release notes, testing new tools (such as Karpenter or Gateway API) in sandbox clusters before recommending them.

## 15.3 Questions to ask the interviewer (general)

* What are the biggest reliability or scaling bottlenecks on the platform over the next twelve months?
* How are cluster boundaries, multi-tenancy and deployments organized today, and where do product teams feel the most friction?
* How are SLOs and error budgets used in practice when prioritizing reliability work against features?
* What does success in the first ninety days look like for this role?

## 15.4 Final checklist (general)

* **AWS:** security groups versus NACLs, ALB versus NLB, target groups, nginx timeouts and real IP, IAM roles, VPC CNI, EC2 families, Nitro limits, ASGs, Spot, IMDSv2, EBS, S3, RDS Multi-AZ.
* **Terraform:** configuration vs state vs plan vs reality, remote state and locking, for_each, lifecycle, modules, data-driven cells, safe rollouts across cells, Terraform vs CloudFormation.
* **Kubernetes:** pods, deployments, StatefulSets, services, ingress, requests vs limits, probes, graceful shutdown, RBAC, network policies, IRSA/Pod Identity, Karpenter, HPA, PDBs, upgrades.
* **Observability and incidents:** Prometheus, Grafana, Loki, Splunk, OpenTelemetry, SLOs and burn rate, alert fatigue, mitigate first, generative AI triage with guardrails.
* **Databases and design:** slow query method, indexes, locks, Blue/Green upgrades, online schema changes, Redis, cell architecture, DR (RTO, RPO, delayed replica), resilience patterns.

## 15.5 Questions to ask the architect or platform lead

* What is the current split across EC2, ECS and EKS, and what is driving the move to EKS?
* How many clusters do you run today, how are they divided (by cell, environment, region or tenant), and where does fleet management hurt most?
* What is the current deployment path (Argo CD, Spinnaker, Helm) and how far along is the golden-chart or paved-road model?
* Which workloads are hardest to run on EKS today—stateless services, stateful systems or data and analytics tools—and why?
* If I joined, what is the one architectural problem you would want me to own in the first quarter?

## 15.6 Checklist for the architect round

* **EKS and fleet:** control plane vs data plane, add-on lifecycle, VPC CNI and IP limits, cluster boundaries, multi-AZ, multi-region, multi-tenancy, in-place vs blue/green upgrades, fleet rings.
* **Service onboarding:** production container, Deployment/PDB/probes/shutdown, RBAC and IRSA/Pod Identity, ingress and egress, network policies, secrets, observability, load test, PRR gate.
* **Delivery and packaging:** golden Helm charts, Argo CD ApplicationSets, Spinnaker vs Argo CD, progressive delivery, supply chain signing and admission policy.
* **Autoscaling and data tools:** HPA on request rate, KEDA, Karpenter NodePools and consolidation, headroom pods, running JupyterHub/Airflow/ShinyProxy/Airbyte on dedicated pools.
* **Networking and mesh:** DNS and ndots, ExternalDNS, cert-manager, Gateway API vs Ingress, Istio resources, response flags, mTLS migration, when not to use a mesh.
* **Reliability and scale:** 16 scale failure modes, zero-downtime 100-cluster upgrades, AZ loss, DR drills, air-gapped clusters, migrating from ECS to EKS.

---

# Part 16: Configuration management with Ansible and immutable infrastructure

## 16.1 Where Ansible fits alongside Terraform and Packer

Infrastructure automation splits cleanly across three layers, and interviewers frequently ask how they work together without stepping on each other:

| Layer | Tool | Responsibility |
| :--- | :--- | :--- |
| **Provisioning** | Terraform | Creates cloud resources: VPCs, subnets, IAM roles, RDS, EKS clusters, EC2 instances, load balancers |
| **Image baking** | Packer + Ansible | Builds immutable AMIs with OS hardening, base packages, monitoring agents, and runtime dependencies pre-installed |
| **Configuration & orchestration** | Ansible | Configures OS settings, manages fleet configuration where servers are long-lived, orchestrates rolling restarts or bare-metal/network devices |

**Agentless push model.** Ansible requires no daemon on target hosts. A control node connects over SSH (Linux) or WinRM (Windows), copies small Python modules over, executes them, and removes them. That makes it easy to adopt on existing fleets and network appliances, though at thousands of hosts you must tune concurrency (`forks`), SSH pipelining, and mitogen or pull mode (`ansible-pull`) so the control node does not become a bottleneck.

**Immutable vs mutable infrastructure.** For stateless cloud tiers, the preferred pattern is **Packer running Ansible** to bake a golden AMI, followed by Terraform updating a launch template and running an ASG instance refresh or Karpenter node expiration. Configuration management still matters for: baking those images cleanly, configuring stateful or legacy EC2 fleets that cannot be replaced casually, configuring bare-metal/air-gapped nodes, and automating network devices (switches/routers via network modules).

## 16.2 Ansible architecture: inventory, playbooks, roles and idempotency

* **Inventory:** defines target hosts and groups. In cloud environments, never maintain static IP lists—use **dynamic inventory plugins** (such as `amazon.aws.aws_ec2`) that query AWS APIs and group instances automatically by tags (`tag_Environment_prod`, `tag_Role_nginx`, `placement_availability_zone`).
* **Playbooks and tasks:** YAML files mapping host groups to ordered lists of tasks. Every task calls a module (`apt`/`dnf`, `copy`, `template`, `systemd`, `user`, `uri`).
* **Roles and Collections:** a **role** packages tasks, handlers, Jinja2 templates, files, defaults, and variables into a reusable unit (`roles/nginx/`, `roles/node_exporter/`). **Collections** distribute curated modules and roles (e.g., `amazon.aws`, `community.general`).
* **Idempotency (the core principle):** running a playbook once or ten times must leave the system in the exact same desired state, reporting `changed` only when an actual modification was required. Use declarative modules (`lineinfile`, `template`, `systemd`) rather than raw `shell` or `command` tasks; when `shell` is unavoidable, guard it with `creates:`, `removes:`, or `changed_when:`.
* **Variable precedence (simplified):** role `defaults` (lowest, easily overridden) -> inventory group/host vars -> playbook `vars` -> role `vars` -> `--extra-vars` (`-e`, highest, always wins). Keep environment overrides in inventory `group_vars/` and sensitive values encrypted.

## 16.3 Secrets, handlers, templates and safe rollouts

* **Ansible Vault:** encrypts sensitive files or individual variables (`ansible-vault encrypt_string`) at rest in Git using AES-256. In CI/CD, supply the vault password via a short-lived secret from AWS Secrets Manager or CI secret storage—or better yet, fetch secrets dynamically at runtime via lookup plugins (`amazon.aws.aws_secret`) so secrets never sit in Git at all.
* **Handlers:** tasks triggered via `notify:` only when a preceding task actually changed something (for example, restarting or reloading `nginx` only when `nginx.conf` changed). Handlers run once at the end of a play, avoiding unnecessary service restarts.
* **Jinja2 templates (`.j2`):** render configuration files dynamically from inventory facts and variables, with `validate:` attributes (such as `validate: 'nginx -t -c %s'`) so Ansible refuses to overwrite a live config if the rendered file has a syntax error.
* **Safe rolling updates across a fleet:**
  * `serial: "20%"` (or `serial: [1, 5, "25%"]` for a canary batch) processes hosts in waves rather than all at once.
  * `max_fail_percentage: 10` aborts the rollout automatically if failures exceed the threshold.
  * `pre_tasks` and `post_tasks` with `delegate_to: localhost` (or load balancer APIs) deregister a node from its target group, wait for drain, apply the update, run a health check (`uri` module), and re-register it.

```yaml
- name: Rolling update of edge nginx fleet
  hosts: tag_Role_nginx
  become: true
  serial: [1, "25%"]                 # canary 1 host first, then 25% waves
  max_fail_percentage: 10
  tasks:
    - name: Render nginx configuration and validate syntax before applying
      ansible.builtin.template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
        owner: root
        group: root
        mode: "0644"
        validate: "nginx -t -c %s"
      notify: Reload nginx

  handlers:
    - name: Reload nginx
      ansible.builtin.service:
        name: nginx
        state: reloaded
```

## 16.4 Ansible in CI/CD and common interview questions

* **Testing and CI quality gates:** `ansible-lint` for style and anti-patterns, `ansible-playbook --syntax-check`, `--check --diff` (dry run showing exact file diffs before touching production), and **Molecule** (spins up ephemeral Docker containers or EC2 instances, converges the role, runs Testinfra/assert verification, and verifies idempotency by running a second converge expecting zero changes).
* **Troubleshooting slow Ansible runs:** enable SSH pipelining (`pipelining = True`), enable `ControlMaster` connection multiplexing, tune `forks` (default is 5, too low for large fleets), disable `gather_facts` when host facts are not needed (or cache facts in Redis/JSON), and use `async` with `poll` for long-running package updates.
* **Say it like this.** "I use Terraform to provision cloud infrastructure, Ansible inside Packer to bake immutable golden AMIs, and standalone Ansible with dynamic AWS inventory, `serial` canary waves, `validate` checks, and `--check --diff` in CI when managing configuration on long-lived hosts or network gear."

---

# Part 17: CI/CD pipelines, containers and cloud-native architecture patterns

## 17.1 CI/CD pipeline design (GitHub Actions, GitLab CI, Jenkins)

Modern DevOps interviews expect you to design an end-to-end delivery pipeline from commit to production, covering security, speed, artifact immutability, and rollback.

**Anatomy of a production CI/CD pipeline:**

1. **Pull Request (PR) / Merge Request (MR) gates (fast feedback, under 5–10 min):**
   * Static analysis, formatting, linting, unit tests, and dependency vulnerability scanning (SCA).
   * Infrastructure/manifest checks: `terraform fmt -check`, `terraform validate`, `tfsec`/`checkov`, `helm lint`, `kubeconform`.
   * Ephemeral preview environment or `terraform plan` posted as a PR comment for peer review.
2. **Main branch / Build stage (build once, promote everywhere):**
   * Run integration tests.
   * Build the container image cleanly (multi-stage Dockerfile, deterministic lockfiles).
   * Scan the built image (Trivy/Grype/ECR Enhanced Scanning); fail the build on critical unpatched CVEs.
   * Generate an SBOM and sign the image digest (Cosign) with build provenance (SLSA).
   * Push to private registry (ECR) tagged with the Git commit SHA (never rely on mutable `latest` tags).
3. **Continuous Delivery / Promotion (dev -> staging -> canary -> prod):**
   * **Authentication:** pipelines authenticate to AWS using **OIDC federation** (GitHub Actions OIDC / GitLab OIDC -> `sts:AssumeRoleWithWebIdentity`) with short-lived tokens scoped to the repository and branch—zero static AWS keys stored in CI secrets.
   * **Deployment trigger:** update the image digest in the GitOps repository (Argo CD) or trigger a parameterized Spinnaker pipeline.
   * **Progressive verification:** run automated smoke tests and synthetic checks against staging; in production, shift traffic gradually (canary 5% -> 25% -> 100%) watching SLO burn rates, rolling back automatically on degradation.

**Speeding up slow pipelines:** cache dependencies and Docker BuildKit layers (`--cache-from`/`--cache-to`), parallelize independent test suites and matrix builds, run ephemeral self-hosted runners on spot instances (e.g., Actions Runner Controller on EKS) with isolated network policies, and separate fast PR checks from heavier nightly regression suites.

## 17.2 Docker and container internals deep dive

Senior interviewers frequently probe beneath `docker build` to see if you understand how containers actually work on Linux and how to build secure, minimal images.

* **What a container really is:** just a regular Linux process (or group of processes) isolated from the rest of the host by kernel features:
  * **Namespaces** restrict *what the process can see*: `pid` (its own process tree starting at PID 1), `net` (its own network interfaces, routing table, ports), `mnt` (its own filesystem mount points), `uts` (hostname), `ipc` (shared memory), and `user` (maps container root UID 0 to an unprivileged host UID).
  * **Control Groups (cgroups v2)** restrict *how much the process can use*: CPU shares/quotas (`cpu.max`), memory limits (`memory.max`—exceeding triggers the kernel OOM killer), and I/O bandwidth.
  * **Capabilities & Seccomp:** Linux splits root privileges into distinct capabilities (`CAP_NET_BIND_SERVICE`, `CAP_SYS_ADMIN`, etc.). Best practice is `drop: ["ALL"]` and add back only what is strictly required, paired with a seccomp profile blocking dangerous syscalls.
* **Union filesystems (OverlayFS):** images are stacks of immutable read-only layers (`lowerdir`), topped by a thin writable copy-on-write layer (`upperdir`) when the container starts. Modifying an existing file copies it up to `upperdir` first; deleting a file creates a "whiteout" file. High-churn writes should go to a mounted volume rather than the container writable layer.
* **Multi-stage builds and minimal base images:**

```dockerfile
# Stage 1: build in a full SDK image
FROM golang:1.23-alpine AS builder
WORKDIR /src
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-s -w" -o /app/server ./cmd/server

# Stage 2: copy only the static binary into a distroless or minimal runtime image
FROM gcr.io/distroless/static-debian12:nonroot
COPY --from=builder /app/server /server
USER 65532:65532
EXPOSE 8080
ENTRYPOINT ["/server"]
```

* **Why multi-stage + distroless matters:** removes compilers, shells (`sh`/`bash`), `curl`, and package managers from production containers—shrinking image size from ~800 MB to ~15 MB (dramatically faster EKS scale-outs), cutting CVE surface area, and preventing attackers who achieve code execution from easily downloading tools or spawning an interactive shell.
* **PID 1 and signal handling:** inside a container, the entrypoint runs as PID 1, which does not automatically forward signals (`SIGTERM`) to child processes or reap zombie processes unless it handles signals properly. Always use the **exec form** (`ENTRYPOINT ["/server"]`) rather than the shell form (`ENTRYPOINT /server`, which wraps in `/bin/sh -c` and swallows `SIGTERM`, causing Kubernetes to wait 30 seconds and send `SIGKILL`).

## 17.3 AWS serverless, messaging and managed data patterns

Even in Kubernetes-heavy roles, cloud infrastructure architects expect fluency in AWS managed integration services so you do not over-engineer everything inside a cluster:

| Service | What it does | Key operational details to mention |
| :--- | :--- | :--- |
| **SQS (Simple Queue Service)** | Managed message queue for decoupling producers and consumers | Standard (at-least-once, best-effort order, near-unlimited throughput) vs FIFO (strict order, exactly-once deduplication, capped TPS). Tune **visibility timeout** longer than max processing time; always attach a **Dead-Letter Queue (DLQ)** with `maxReceiveCount` and alarm on DLQ depth. Ideal trigger for KEDA pod autoscaling. |
| **SNS (Simple Notification Service)** | Pub/sub fan-out to many subscribers (SQS queues, Lambda, HTTP endpoints) | Fan-out pattern: publish once to SNS -> deliver to multiple independent SQS queues so each downstream service processes at its own pace and retries independently. |
| **EventBridge** | Serverless event bus with schema registry and content-based routing rules | Routes AWS service events (EC2 spot interruptions, GuardDuty findings, Health events) and custom SaaS events to Step Functions, Lambda, or SQS. Supports event replay and archiving. |
| **AWS Lambda** | Event-driven serverless compute (up to 15 min runtime) | Great for glue automation (remediation hooks, custom rotation Lambdas, S3 event processing). Watch **cold starts** (mitigate with SnapStart or Provisioned Concurrency), **reserved concurrency** (protects downstream RDS from sudden Lambda scale-out floods), and VPC ENI attachment limits. |
| **DynamoDB** | Serverless single-digit-millisecond NoSQL key-value/document store | Scales via partition keys—choose high-cardinality partition keys to avoid **hot partitions**. On-demand vs provisioned capacity with autoscaling; Global Tables for active-active multi-region replication; TTL for automatic item expiration; DynamoDB Streams for change-data-capture. |
| **API Gateway** | Managed front door for REST, HTTP, and WebSocket APIs | Built-in throttling/usage plans, JWT/Cognito/Lambda authorizers, request validation, and private VPC Link integration to internal ALBs/NLBs. |

## 17.4 High-level system design playbook for DevOps and platform roles

When given an open-ended architecture prompt ("Design a global CI/CD platform", "Design a multi-region URL shortener / metrics ingestion pipeline / secrets platform"), use this structured 5-step cadence so you cover every dimension senior interviewers score:

1. **Clarify scope & quantify back-of-the-envelope numbers (3–4 min):**
   * Functional requirements (read vs write ratio, sync vs async, multi-tenancy).
   * Non-functional requirements: availability target (99.9% vs 99.99%), latency SLO (p99 < 100 ms), RPO/RTO, compliance/data residency.
   * Rough math: e.g., $10{,}000\text{ RPS} \approx 8.6 \times 10^8\text{ requests/day}$; at $1\text{ KB}$ per event, that is $\sim 860\text{ GB/day}$ of storage. Knowing whether data is MBs, GBs, or PBs immediately dictates storage and network choices.
2. **High-level architecture (end-to-end request flow, 5–7 min):**
   * Draw the path cleanly: **Edge** (Route 53, CloudFront, WAF) -> **Ingress** (ALB/NLB, API Gateway) -> **Compute** (EKS stateless pods with HPA/Karpenter or ECS/Lambda) -> **Async backbone** (SQS/Kafka for burst absorption and decoupling) -> **Data & Cache** (Redis for hot reads, Multi-AZ RDS/DynamoDB for durable state, S3 for blobs/archives).
3. **Deep dive into bottlenecks & scaling (5–7 min):**
   * How does each tier scale horizontally? Where is the single point of failure or write bottleneck?
   * Address caching strategy (cache-aside, TTL jitter, stampede protection), connection pooling (RDS Proxy), database read replicas/partitioning/cells, and backpressure/rate limiting at the edge.
4. **Reliability, security & disaster recovery (4–5 min):**
   * Multi-AZ by default (at least 3 AZs, PDBs, topology spread); multi-region strategy (active-active for stateless/DynamoDB Global Tables, or cell-based active-passive with cross-region replicas and tested RPO/RTO).
   * Zero-trust security: IAM least privilege (IRSA/Pod Identity), TLS everywhere, KMS encryption at rest, Secrets Manager rotation, network segmentation (private subnets, SGs, NetworkPolicies).
5. **Day-2 operations, observability & cost (3–4 min):**
   * Golden signals (metrics, structured logs, distributed traces), user-facing SLO burn-rate alerts, automated canary deployments with rollback, and FinOps levers (Graviton, Spot for fault-tolerant workers, VPC endpoints to eliminate NAT data charges, storage lifecycle tiers).
