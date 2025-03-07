---
sidebar_label: "FAQ"
sidebar_position: 4
---

# Frequently Asked Questions

## How do I start using Capact?

To learn how to begin your adventure with Capact, check the [Getting Started](./getting-started.mdx) document.

## How do I troubleshoot Capact installation?

First, check out [a list of common problems](./operation/common-problems.md) that you may encounter. Next, read the [Basic diagnostics](./operation/diagnostics.md) guide and execute diagnostic actions which may help you find bug causes.

If you found a bug, please report it or contribute a fix. To do so, read our [Contribution guide](/community/contributing). We are open for any type of contributions! 

## How does Capact compare to...

### Kubevela with Crossplane

Kubevela is a tool to describe and ship applications. Kubevela's core is built on top of Crossplane, and it uses Open Application Model (OAM). In Crossplane you define application resources with [Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/).
There are many similarities between Capact and Kubevela. Both can deploy and manage diverse workload types such as container, databases, EC2 instances across hybrid environments. Both solutions work as glue which can connect different tools like Terraform and Helm.

There are few differences between them:

1. Kubevela uses declarative API to describe application, its configuration and dependencies. Capact is using workflow-based approach. We believe that it makes Capact more flexible, especially for day-2 operations.
    For example, with Capact you can create an advanced workflow for doing a backup. In the workflow first you pause an application, create volume snapshot, create DB snapshot, copy snapshot to S3 bucket and rotate the previous backups.

1. Capact has interchangeable dependencies as a built-in feature. Dependencies are described using Interfaces. You can configure Implementation preferences for any Interface with [Policies](./feature/policies/overview.md) to select Implementation based on an Interface while managing applications. For example, if your application depends on SQL database, for local development, you can prefer to use in-cluster PostgreSQL installed by Helm, but for production environment you prefer managed solution such as AWS RDS.

1. With Kubevela and Crossplane you can provision infrastructure and deploy applications. Using Capact you can do the same, but it goes beyond that. With workflow based approach you can use it for anything. You can have action which runs data processing, which runs diagnostics, you can create advanced backup process or even do machine learning.

### Helm

Helm is a package manager for Kubernetes. Capact uses [Helm runner](https://github.com/capactio/capact/tree/main/cmd/helm-runner/README.md) to install applications in Kubernetes. Capact goes beyond Kubernetes and can deploy and manage diverse workloads like AWS RDS or EC2 instances. In a way, Capact extends Helm.

Depending on set [Policies](./feature/policies/overview.md) Capact can use different solutions. For example, if you are deploying an application which is using a database, you may use RDS PostgreSQL and pass required values to the Helm chart or use in-cluster PostgreSQL also installed by Helm.

Helm provides you a way to install, update and delete charts. Capact on the other hand allows you to run multiple day-2 operations, such as doing backups, running diagnostics, etc.

### Operator Framework

Operator Framework is a toolkit to manage Kubernetes application. It makes it easy to do day-1 and day-2 operations. It's easy to use as long all needed actions are available.
Capact is a glue connecting different tools, and it could use Operators to manage Kubernetes applications. For now, we have a runner that supports Helm from the Kubernetes ecosystem, but in future we could also support Operator Framework.

### Terraform, Ansible, Chef, etc.

In general, all these tools are used to describe and enforce the desired state of the environment. As Capact is a layer above of the tools, they can be used as a part of a Capact workflow and even can be mixed. We already have [Terraform runner](https://github.com/capactio/capact/tree/main/cmd/terraform-runner/README.md). Ansible and other runners are also possible.

For example, when running Capact manifests, you can deploy AWS RDS and EKS defined as Terraform modules. Then, using Helm runner, you can deploy Mattermost in your Kubernetes cluster. All this can be done in one OCF manifest. See our [Mattermost example](./example/mattermost-installation.md) for more details.

### Pulumi

Capact supports Terraform runner to use Terraform modules to manage your infrastucture. Pulumi is similar to Terraform, however, instead of having its configuration language, you can use programming languages like Python, Go, JavaScript and others. There could be a Pulumi runner for Capact, which allows you to use Pulumi content in OCF manifests.

## What is the origin of name “Capact”?

Capact is a combination of two shortened words: “**cap**ability” and “**act**ion”. Capact makes it easy to manage system capabilities via running Actions. In the end, everything boils down to actions. Actions can provision infrastructure, can deploy applications, can process data. Once you start using Capact, the possibilities are virtually endless.
