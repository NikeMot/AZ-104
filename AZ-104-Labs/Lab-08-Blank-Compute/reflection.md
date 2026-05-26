# Lab 08 Reflection

## What this lab proved

This lab proved that compute service selection can be done from business requirements without a guided walkthrough.

The key skill was converting workload requirements into Azure compute choices.

## VM vs App Service

A VM is appropriate when the workload needs OS-level control, custom software, or legacy server behavior.

App Service is appropriate when the workload is a web application and the goal is to avoid managing the underlying OS.

```text
Need OS control = VM
Need managed web hosting = App Service
```

## VMSS vs Availability Set

A VMSS manages a scalable group of similar VM instances.

An availability set protects manually managed VMs across fault and update domains.

```text
Need autoscaling identical instances = VMSS
Need rack/update-domain resiliency = availability set
```

## ACI vs Container Apps

ACI runs a simple container quickly with minimal platform complexity.

Container Apps provides managed app-style container hosting with ingress, scaling, and revisions.

```text
Simple container = ACI
Managed scalable container app = Container Apps
```

## ACR vs ACI/Container Apps

ACR stores images. It does not run containers.

ACI and Container Apps run containers.

```text
ACR = image registry
ACI/Container Apps = runtime platforms
```

## App Service Plan vs App Service App

The App Service plan controls compute, scale, tier, and features.

The App Service app is the hosted web application.

```text
Plan = workers/scale/cost/features
App = web workload
```

## Scale Up vs Scale Out

```text
Scale up = bigger worker/tier
Scale out = more instances
```

## Deployment Slots vs Scaling

Deployment slots are for release safety, staging, swap, and rollback.

They do not add production serving capacity like scale-out does.

```text
Slots = deployment strategy
Scale-out = capacity strategy
```

## VNet Integration vs Private Endpoint

VNet integration allows outbound access from App Service into a VNet.

Private endpoint allows private inbound access to App Service.

```text
VNet integration = outbound from app
Private endpoint = inbound to app
```

## ARM/Bicep Value

ARM/Bicep provides repeatable, reviewable, parameterized deployment.

It reduces reliance on portal-only manual builds and supports consistent environments.

```text
Manual portal build = harder to repeat
ARM/Bicep = repeatable desired state
```

## What would change in production

A production design would likely include:

```text
naming standards
tagging standards
managed identities
Key Vault integration
Azure Monitor alerts
Log Analytics diagnostics
backup/restore testing
private endpoints for sensitive PaaS services
CI/CD deployment pipelines
Bicep modules
policy enforcement
cost budgets
```

## Exam readiness judgement

This lab strengthens AZ-104 readiness because compute questions often ask:

```text
Which service best meets this workload requirement?
Which scaling method is correct?
Which availability feature matches the failure model?
Which App Service networking feature solves the direction of access?
Which container service is appropriate?
```

The compute domain is ready when those decisions become automatic.
