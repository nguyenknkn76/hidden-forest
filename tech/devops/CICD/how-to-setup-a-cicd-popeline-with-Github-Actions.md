# How to set up a CI/CD pipeline with GitHub Actions for Aitomated Deployments

## What is a CI/CD pipeline?
It automatse the process of building, testing, and deploying code whenever changes are mede to a repo.
- Continuous Integration (CI): ensures that new code is automatically tested and merged.
- Continnuous Delivery (CD): automates deployment, making sure the lastest version of the software is always ready for release.

## Why Do We Need It?
Without CI/CD: dev must manually test and deploy code
=> CI/CD pipeline speeds up the dev cycle, reduces bugs, and ensures a smooth deployment process.
A project hosted on `VPS`:
- With CI: every time u push code to GitHub, it automatically runs tests to check for errors
- With CD: if all tests pass, ur app automatically deploys to VPS, keeping it up-to-date without manual intervention.

## How Does It Work?
### Principles:
### Do it step-by-step:
- Step 1: Create Nodejs project
- Step 2: Create a GitHub Repository
  - Init a Git repo
  - Push project to Git
- Step 3: Set Up Secret Variables in GitHub
- Step 4: Create the GitHub Actions Workflow
- Step 5: Set Up runners
  - GitHub-Hosted Runners
  - Self-Hosted Runners
  - Follow these steps:
1. Go to GitHub repo.
2. Click on Settings tab.
3. Choose Actions → Runners
4. Click on the `New self-hosted runner` button.
5. Choose the runner image
6. Copy & paste the setup commands provided by GitHub into ur server terminal to register the runner with ur repo or organization
- Step 6: Test CI/CD Pipeline
Now that everything is setup:
1. Make a change in Nodejs project.
2. Push it to the main branch of Git repo.
3. Navigate to the Actions tab in ur Git repo and observe the workflow.
4. (if everything is setup correctly) GitHub Actions will SSH into ur VPS and deploy the lastest code automatically.

> Read more: https://dev.to/vishnusatheesh/how-to-set-up-a-cicd-pipeline-with-github-actions-for-automated-deployments-j39 

