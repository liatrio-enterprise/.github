# Liatrio's GitHub Enterprise Foundations
V1: This example Github Organization illustrates Liatrio's opinionated approach for businesses looking to setup a foundational infrastructure in Github Enterprise to manage teams, repositories, and branch policies.

V2: This space is a demonstration of Liatrio's opinionated approach to laying a foundation for managing multiple product teams in a single GitHub org in a robust, secure, and repeatable way.

### [Team Management](https://github.com/liatrio-enterprise/azure-github-adgroup-team-terraform)
Teams in GitHub are the primary organization unit under the Org itself. 
Teams can be used to manage access to repositories, and can be linked to IdP (identity provider, such as Azure Active Directory or Okta) groups to allow easy enterprise-scale management of group membership.

We have found Terraform to be a good way to manage GitHub teams; it can create the teams, associate them with IdP groups, and even create the IdP groups if desired. 

### CI/CD Build Infrastructure / Self-hosted Runners
#### [Infrastructure](https://github.com/liatrio-enterprise/github-runner-infrastructure)
Many businesses will want to host their own CI/CD infrastructure, whether for unique tool requirements, or to access resources that are on internal networks.
We have found Kubernetes to be a good solution for self-hosting runners, as the [actions runner controller](https://github.com/actions-runner-controller/actions-runner-controller) project allows for scaling runners easily.
We deploy our cluster and configure runners on it using Terraform and Terragrunt.

#### [Builder images](https://github.com/liatrio-enterprise/runner-images)
We have built some docker images that are tailored to our workflows. The images are built on GitHub actions and pushed to GitHub Container Registry, where they are available to our cluster and runners.

#### [Reusable Workflows](https://github.com/liatrio-enterprise/github-workflows)
Most enterprises will have some common patterns in their build systems; often it makes sense to extract that common functionality into a shared workflow.

### [Repository/Branch Protections](https://github.com/liatrio-enterprise/github-policy-service)
GitHub makes it easy to create new repositories, which makes getting started with new projects accessible, but can make enterprise management a challenge.
We found that using a GitHub App can help with this, in that it can react to events such as repo creation or branch creation, and immediately bring new repos under enterprise standards.
Our GitHub app is listening to a variety of events, and makes sure that our standard branch policies are applied to each repo's `main` branch at all times.

Our App is deployed to Azure App Service which was created by Terraform.

### [Migrations](https://github.com/liatrio-enterprise/github-migration-azure-devops)
Migrations from one platform to another are often chaotic and slow, but automation can make the process somewhat less painful.
This repository contains a workflow that helps with migrating from Azure DevOps to GitHub, by importing all the repositories from an Azure DevOps project to GitHub in a standardized way.
It can also be used to assign all the repos to the appropriate team in GitHub.