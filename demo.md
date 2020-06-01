# Demo - GitHub Action

## 1. Briefly explain what GitHub Action is

#### Action: Individual tasks
#### Workflow: Custom CI/CD Pipeline created with multiple actions

    1. What is GitHub Actions?
    2. What can we achieve with GitHub Actions?
    3. What are some features of GitHub Actions?
    4. Usage Limit, GitHub Enterprise, Cost
  
####   Apparently GitHub Action is not supported yet on self-hosted version of GitHub Enterprise

## 2. GitHub Action vs GitLab CI

#### As you can see, GitHub Actions has most of the features GitLab CI has

## 3. How to implement a Workflow file?

#### Explain on what each attributes indicate in the workflow file

## 4. What else can we do with GitHub Action?

## 5. Short Demo on implementing a workflow for deploying Heroku web app using Python Flask

### This repository has all the dependencies and application installed for Python Flask app which is deployed on Heroku server
    In the src directory, there is a app.py file which just returns "Hello, World!" when we use the app
    In the tests directory, there is test_app.py file which checks if the index returns "Hello, World!"
    Then there are other files which are just requirements and dependencies for the application

### In this demo, I will be creating a workflow based on the Action for Python application provided in the Marketplace
    The workflow will be triggered when the code has been pushed or pull request has been made to the master

### In the workflow, we will be executing the following tasks:

#### For Continuous Integration:
    1. Checkout from master and make a deep clone of the repository
    2. Set up Python 3.8
    3. Install the dependencies required for testing
    4. Lint with Flake 8
    5. Test the code with Pytest

#### For Continuous Deployment:
    1. Deploy the code to Heroku server, only if the previous tasks were successful
