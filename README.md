# Day 40 – My First GitHub Actions Workflow

## Objective

The goal of this task is to understand how GitHub Actions works and create the first CI workflow that runs automatically when code is pushed to the repository.

This exercise demonstrates how CI/CD automation starts with a simple workflow.


# What is GitHub Actions?

GitHub Actions is a CI/CD automation platform that allows developers to build, test, and deploy code automatically when events occur in a repository.

Example events include:

* Code push
* Pull request creation
* Scheduled tasks
* Manual trigger

GitHub Actions workflows run on **GitHub-hosted runners**, which are virtual machines that execute automation steps.


# Workflow Execution Flow

Developer pushes code


GitHub detects event


Workflow triggers


Runner (Ubuntu VM) starts


Steps execute


Pipeline result (Success / Failed)


# Task 1 – Repository Setup

## Step 1 – Create Repository

Create a new **public GitHub repository** named:

github-actions-practice


## Step 2 – Clone Repository

Clone the repository locally:

cd github-actions-practice

## Step 3 – Create Workflow Folder

GitHub Actions workflows must be stored in a specific directory.

Create the required structure:

.github/workflows/

Command:

mkdir -p .github/workflows

Repository structure should look like:

github-actions-practice
.github
  workflows

# Task 2 – Create Hello Workflow

Create the workflow file:

.github/workflows/hello.yml

Add the following workflow configuration.

name: Hello Workflow

on: push

jobs:
  greet:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Print Hello
        run: echo "Hello from GitHub Actions!"

# Explanation of Workflow

## name

Defines the workflow name that appears in the GitHub Actions interface.

Example:

name: Hello Workflow

## on

Defines the event that triggers the workflow.

on: push

This means the workflow runs whenever code is pushed to the repository.


## jobs

A workflow contains one or more jobs.

jobs:
  greet:

Here **greet** is the job name.

## runs-on

Defines the environment where the job runs.

runs-on: ubuntu-latest

GitHub creates an Ubuntu virtual machine to run the job.

## steps

Steps define the sequence of tasks executed in the job.

Each step performs a specific action.

## uses

Used to run a prebuilt GitHub Action.

uses: actions/checkout@v4

This action checks out the repository code to the runner.

## run

Executes shell commands inside the runner environment.

run: echo "Hello from GitHub Actions!"

# Push the Workflow

Add and commit the workflow file:

git add .
git commit -m "Add first GitHub Actions workflow"
git push origin main

After pushing, open the repository and go to:

Actions tab

The workflow will run automatically.

If successful, the pipeline will show a **green check mark**.


# Task 3 – Understanding Workflow Anatomy

The workflow contains several important components:

Keyword | Description 

name - Defines the workflow name     
on - Defines the trigger event    
jobs - Defines tasks executed in workflow 
runs-on - Specifies the runner environment 
steps - Defines sequence of actions   
uses -    Executes reusable GitHub Actions   
run -    Runs shell commands                

Understanding these components is essential for building CI/CD pipelines.

# Task 4 – Add More Workflow Steps

Update the workflow to include additional steps that display system information.

Updated workflow:

name: Hello Workflow

on: push

jobs:
  greet:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Print Hello
        run: echo "Hello from GitHub Actions!"

      - name: Print Current Date
        run: date

      - name: Print Branch Name
        run: |
          echo "Branch: ${{ github.ref_name }}"

      - name: List Files
        run: ls -la

      - name: Show Runner OS
        run: uname -a

## What These Steps Do

Print Date
Displays the current system time.

Print Branch
Displays the branch that triggered the workflow.

List Files
Lists all files in the repository.

Show Runner OS
Displays information about the runner's operating system.

# Task 5 – Break the Pipeline Intentionally

To understand pipeline failures, a step is added that causes the workflow to fail.

Example step:


- name: Break Pipeline
  run: exit 1
  
Full example:
- name: Break Pipeline
  run: exit 1
  
Push the changes:

git add .
git commit -m "Break pipeline intentionally"
git push

The pipeline will fail.

GitHub Actions will display the failed step in red.

# Understanding Pipeline Failure

CI pipelines fail when a command returns a non-zero exit code.

# Fixing the Pipeline

Remove the failing step and push again.


git add .
git commit -m "Fix pipeline"
git push

The pipeline should run successfully again.

# Final Repository Structure

github-actions-practice

 .github
    workflows
     hello.yml
 README.md
 
# What I Learned

* Basics of GitHub Actions
* Creating the first CI workflow
* Understanding workflow structure
* Running commands inside runners
* Using GitHub variables
* Observing pipeline success and failure
* Debugging CI pipelines


# Conclusion

This exercise demonstrated how CI pipelines work using GitHub Actions.

Even a simple workflow provides insight into how automation runs in the cloud.
Understanding these fundamentals is essential for building advanced CI/CD pipelines used in real-world DevOps environments.
