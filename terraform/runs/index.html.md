---
title: "About Terraform Runs in Atlas"
---

# About Terraform Runs in Atlas

A "run" in Atlas represents the logical grouping of two Terraform steps - a
"plan" and an "apply". The distinction between these two phases of a Terraform
run are documented below.

When a [new run is created](/help/terraform/runs/starting), Atlas
automatically queues a Terraform plan. Because a plan does not change the state
of infrastructure, it is safe to execute a plan multiple times without
consequence. An apply executes the output of a plan and actively changes
infrastructure. You can read more about Terraform plans and applies below.

## Plan

During the plan phase of a run, Atlas executes the command `terraform plan`.
Terraform performs a refresh and then determines what actions are necessary to
reach the desired state specified in the Terraform configuration files. A
successful plan outputs an executable file that is securely stored in Atlas
and may be used in the subsequent apply.

Terraform plans in Atlas do not change the state of infrastructure, so it is
safe to execute a plan multiple times. In fact, there are a number of components
in Atlas that can trigger a Terraform plan. You can read more about this in the
[starting runs](/help/terraform/runs/starting) section.

## Apply

During the apply phase of a run, Atlas executes the command `terraform apply`
with the executable result of the prior Terraform plan. This phase **can change
infrastructure** by applying the changes required to reach the desired state
specified in the Terraform configuration file.

While Terraform plans are safe to run multiple times, Terraform applies often
change active infrastructure. Because of this, the default behavior for Atlas
is to require user confirmation as part of the
[Terraform run execution](/help/terraform/runs/how-runs-execute). Upon
user confirmation, Atlas will queue and execute the Terraform apply. It is also
possible to configure Atlas to
[automatically apply](/help/terraform/runs/automatic-applies), but this option is
disabled by default.

To receive alerts when user confirmation is needed or for any other phase of the
run process, you can
[enable run notifications](/help/terraform/runs/notifications) for your
organization or environment.
