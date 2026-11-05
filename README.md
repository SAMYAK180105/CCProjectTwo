# Automated Deployment of a Serverless Student Task Management Application Using Terraform-Based Infrastructure as Code

## Project Overview

This project demonstrates the implementation of a serverless Student Task Management Application using **Infrastructure as Code (IaC)** with Terraform and Cloudflare.

The application enables students to create, view, update, and delete academic tasks through a web-based interface. Task information is stored persistently using Cloudflare Workers KV, while Cloudflare Workers handles application requests and REST API operations.

Instead of manually creating cloud infrastructure, all required resources are defined and provisioned through Terraform configuration files.

The project also integrates GitHub Actions to demonstrate automated infrastructure validation and deployment through a CI/CD workflow.

## Problem Statement

Traditional cloud infrastructure deployment often involves manually configuring compute resources, storage, application settings, and deployment environments.

This approach can lead to configuration errors, inconsistent environments, difficulty in tracking changes, and time-consuming infrastructure recreation.

This project addresses these challenges by implementing Terraform-based Infrastructure as Code to automate the provisioning, modification, destruction, and recreation of cloud infrastructure.

## Objectives

- Implement Infrastructure as Code using Terraform.
- Provision Cloudflare Workers through Terraform.
- Create and manage Cloudflare Workers KV namespaces.
- Establish Worker-to-KV binding.
- Develop a serverless Student Task Management Application.
- Implement REST API-based CRUD operations.
- Maintain infrastructure configuration using Git and GitHub.
- Implement CI/CD using GitHub Actions.
- Demonstrate infrastructure modification, destruction, and recreation.

## System Architecture

```text
              Developer / Student
                      |
                      |
                  Git Push
                      |
                      v
               GitHub Repository
                      |
                      v
                GitHub Actions
                      |
                      v
                  Terraform
                      |
                Cloudflare Provider
                      |
              +-------+-------+
              |               |
              v               v
       Cloudflare Worker   Workers KV
              |               |
              | REST API      | Task Records
              +-------+-------+
                      |
                      v
             Student Task Manager
                      |
                      v
                 Web Browser
```

## Technologies Used

| Component | Technology |
|---|---|
| Infrastructure as Code | Terraform |
| Cloud Platform | Cloudflare |
| Serverless Compute | Cloudflare Workers |
| Data Storage | Cloudflare Workers KV |
| Frontend | HTML, CSS, JavaScript |
| Backend / API | JavaScript (Cloudflare Worker) |
| Version Control | Git |
| Repository Hosting | GitHub |
| CI/CD | GitHub Actions |

## Application Features

### 1. Add Task
Students can create academic tasks by providing:
- Task Title
- Priority (High, Medium, Low)
- Status (Pending, Completed)

### 2. View Tasks
Display all saved tasks with their IDs, titles, priorities, statuses, and creation dates.

### 3. Update Task
Modify existing task information, including task status.

### 4. Delete Task
Remove unwanted tasks from the application.

### 5. Persistent Storage
Store task information using Cloudflare Workers KV.

## REST API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/tasks` | Create a task |
| GET | `/api/tasks` | Retrieve all tasks |
| GET | `/api/tasks/{id}` | Retrieve an individual task |
| PUT | `/api/tasks/{id}` | Update a task |
| DELETE | `/api/tasks/{id}` | Delete a task |

### Example API Request

**POST /api/tasks**

```json
{
  "title": "Submit Project Report",
  "priority": "High",
  "status": "Pending"
}
```

## Project Directory Structure

```text
CCProjectTwo/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── application/
│   ├── worker.js
│   ├── index.html
│   ├── style.css
│   └── script.js
│
├── terraform/
│   ├── providers.tf
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── terraform.tfvars.example
│
├── screenshots/
│
├── .gitignore
│
└── README.md
```

## Infrastructure as Code Implementation

Terraform manages the cloud infrastructure through declarative configuration files.

The infrastructure includes:

1. Cloudflare Worker
2. Cloudflare Workers KV Namespace
3. Worker-to-KV Binding
4. Application Configuration and Variables
5. Terraform Outputs

### Terraform Lifecycle

```text
Define Infrastructure
        |
        v
  terraform init
        |
        v
  terraform fmt
        |
        v
  terraform validate
        |
        v
  terraform plan
        |
        v
  terraform apply
        |
        v
 Infrastructure Created
        |
        v
 Modify Configuration
        |
        v
 Infrastructure Updated
        |
        v
 terraform destroy
        |
        v
 Infrastructure Removed
        |
        v
 Infrastructure Recreated
```

## Installation and Setup

### Prerequisites

- Git
- Terraform CLI
- Cloudflare Account
- Cloudflare API Token
- Cloudflare Account ID
- VS Code or another code editor
- GitHub Account

### Step 1: Clone Repository

```bash
git clone https://github.com/SAMYAK180105/CCProjectTwo.git
```

```bash
cd CCProjectTwo
```

### Step 2: Configure Cloudflare Credentials

Create a Cloudflare API token with the required permissions for managing Workers and KV resources.

Set the following environment variables.

**Windows PowerShell:**

```powershell
$env:CLOUDFLARE_API_TOKEN="YOUR_API_TOKEN"
$env:CLOUDFLARE_ACCOUNT_ID="YOUR_ACCOUNT_ID"
```

Never commit API tokens or credentials to GitHub.

### Step 3: Configure Terraform

Navigate to the Terraform directory:

```bash
cd terraform
```

Initialize Terraform:

```bash
terraform init
```

Format configuration:

```bash
terraform fmt
```

Validate configuration:

```bash
terraform validate
```

### Step 4: Generate Execution Plan

```bash
terraform plan
```

Review the proposed infrastructure changes before applying them.

### Step 5: Provision Infrastructure

```bash
terraform apply
```

Confirm the operation when prompted.

### Step 6: Verify Deployment

Check the Terraform outputs:

```bash
terraform output
```

Verify that the Cloudflare Worker, KV namespace, and Worker-KV binding have been provisioned successfully.

## CI/CD Implementation

GitHub Actions is used to automate the infrastructure deployment workflow.

### CI/CD Workflow

```text
Developer Updates Code
          |
          v
       Git Push
          |
          v
   GitHub Repository
          |
          v
     GitHub Actions
          |
          v
    Checkout Source
          |
          v
   Install Terraform
          |
          v
     Terraform Init
          |
          v
   Terraform Validate
          |
          v
     Terraform Plan
          |
          v
    Terraform Apply
          |
          v
   Cloudflare Deployment
```

Cloudflare credentials should be configured as GitHub Actions repository secrets.

Required secrets:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

## Testing and Validation

The application supports the following functional test cases:

| Test Case | Expected Result |
|---|---|
| Create Task | Task is successfully created |
| View Tasks | Saved tasks are displayed |
| Get Individual Task | Requested task is returned |
| Update Task | Task information is updated |
| Delete Task | Selected task is removed |
| Persistent Storage | Task data remains stored in KV |

## Infrastructure Modification

Terraform is used to modify existing infrastructure by updating configuration values such as Worker names, environment variables, or application settings.

```bash
terraform plan
terraform apply
```

Terraform identifies the differences between the declared configuration and managed infrastructure.

## Infrastructure Destruction

To examine the resources proposed for removal:

```bash
terraform plan -destroy
```

To destroy Terraform-managed infrastructure:

```bash
terraform destroy
```

## Infrastructure Recreation

After destruction, the infrastructure can be provisioned again using the existing Terraform configuration.

```bash
terraform plan
terraform apply
```

This demonstrates the reproducibility and automation capabilities of Infrastructure as Code.

## Security Considerations

- API tokens must not be hardcoded in source files.
- Sensitive credentials must be stored using environment variables or GitHub Secrets.
- Sensitive Terraform variables and state files must not be committed to a public repository.
- Use appropriate API token permissions.
- Review Terraform execution plans before applying changes.

## Learning Outcomes

Through this project, the following concepts are demonstrated:

- Infrastructure as Code fundamentals.
- Declarative infrastructure management.
- Terraform providers, resources, variables, and outputs.
- Terraform initialization, validation, planning, and execution.
- Serverless application deployment.
- Cloudflare Workers and Workers KV integration.
- REST API development and CRUD operations.
- Git and GitHub version control.
- GitHub Actions CI/CD automation.
- Infrastructure modification, destruction, and recreation.

## Future Enhancements

- Student authentication and login.
- Task categories and deadlines.
- Search and filter functionality.
- Priority-based task sorting.
- Task completion statistics.
- Multiple deployment environments (Development, Testing, Production).
- Reusable Terraform modules.

## Project Information

**Project Type:** Mini Project – Infrastructure as Code (IaC)

**Project Title:** Automated Deployment of a Serverless Student Task Management Application Using Terraform-Based Infrastructure as Code

**Developer:** Samyak Dere

**GitHub Repository:** https://github.com/SAMYAK180105/CCProjectTwo

**Cloud Platform:** Cloudflare

**Infrastructure as Code Tool:** Terraform

---

## Conclusion

This project demonstrates how Terraform-based Infrastructure as Code can simplify the deployment and management of serverless cloud applications.

By combining Terraform, Cloudflare Workers, Workers KV, GitHub, and GitHub Actions, the project establishes an automated and reproducible infrastructure deployment workflow.

The primary outcome is demonstrating the complete Infrastructure as Code lifecycle, from infrastructure definition and automated provisioning to modification, destruction, and recreation.

**Infrastructure Definition → Automated Provisioning → Application Deployment → CI/CD → Modification → Destruction → Recreation**
