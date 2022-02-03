# Liatrio's GitHub Enterprise Foundations
This GitHub Organization demonstrates [Liatrio's](https://www.github.com/liatrio) opinionated approach to managing teams, repositories, and continuous policy within GitHub Enterprise. 
The repositories in this Org contain functional reference code and automation for enterprise teams looking to manage their GitHub Organizations in a robust, secure, and repeatable way.

### [Team Management](https://github.com/liatrio-enterprise/azure-github-adgroup-team-terraform)
Teams in GitHub are the primary organization unit under the Org itself. 
Teams can be used to manage access to repositories, and can be linked to IdP (identity provider, such as Azure Active Directory or Okta) groups to allow easy enterprise-scale management of group membership.

We have found Terraform to be a good way to manage GitHub teams; it can create the teams, associate them with IdP groups, and even create the IdP groups if desired. 

### CI/CD Build Infrastructure / Self-hosted Runners
#### [Infrastructure](https://github.com/liatrio-enterprise/github-runner-infrastructure)
Many businesses will want to host their own CI/CD infrastructure, whether for unique tool requirements, or to access resources that are on internal networks.
We have found Kubernetes to be a good solution for self-hosting runners, as the [actions runner controller](https://github.com/actions-runner-controller/actions-runner-controller) project allows for easy runner scaling.
We deploy our cluster and configure runners on it using Terraform and Terragrunt.

#### [Builder images](https://github.com/liatrio-enterprise/runner-images)
We have built some docker images that are tailored to our workflows. The images are built on GitHub actions and pushed to GitHub Container Registry, where they are available to our cluster and runners.

#### [Reusable Workflows](https://github.com/liatrio-enterprise/github-workflows)
Most enterprises will have some common patterns in their build systems; often it makes sense to extract that common functionality into a shared workflow.

### [Repository/Branch Protections](https://github.com/liatrio-enterprise/github-policy-service)
GitHub makes it easy to create new repositories, which makes getting started with new projects accessible, but can make enterprise management a challenge.
We found that using a GitHub App can help with this, in that it can react to events such as repo creation or branch creation, and immediately bring new repos under enterprise standards.


### [Migrations](https://github.com/liatrio-enterprise/github-migration-azure-devops)
Migrations from one platform to another are often chaotic and slow, but automation can make the process somewhat less painful.
We built a workflow that helps with migrating from Azure DevOps to GitHub by importing all the repositories from an Azure DevOps project to GitHub in a standardized way.