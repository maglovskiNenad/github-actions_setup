# Setting up a GitHub action ###

## Manual deploy  React application with GitHub Actions:

* Create the file <code>.github/workflows/deploy.yml</code>.
* Open your GitHub repository.
* Create a directory named <code>.github/workflows/</code> if it doesn't exist, and inside it, add a file named <code>deploy.yml</code>.

      
      name: Manual Deploy to GitHub Pages

      on:
        workflow_dispatch:
          inputs:
            branch:
              description: "Branch to deploy"
              required: true

      jobs:
        deploy:
          runs-on: ubuntu-latest

          steps:
            - name: Checkout Repository
              uses: actions/checkout@v2

            - name: Setup Node.js
              uses: actions/setup-node@2
              with:
                node-version: "14"

            - name: Install Dependencies
              run: npm install

            - name: Build
              run: npm run build

            - name: Deploy to GitHub Pages
              run: |
                git checkout -b gh-pages
                git add -f build
                git config --global user.email "email@address.com"
                git config --global user.name "username"
                git commit -m "Manual Deploy to GitHub Pages"
                git push origin gh-pages


* This example uses the <code>workflow_dispatch</code> event, allowing you to manually trigger the workflow from the GitHub interface. The workflow expects input for selecting the branch you want to deploy.
* To Manually Start the Workflow, go to your GitHub repository.
* Click on "Actions" in the main repository menu.
* Click on "Manual Deploy to GitHub Pages."
* Click the "Run workflow" button and enter the desired branch.
* When you start the workflow, you'll be prompted to enter a value for the branch parameter. Enter the branch name you want to deploy and click the "Run workflow" button.
* Monitor the process.
* This workflow is designed to be triggered manually, giving you control over when to perform the deployment. It allows you to avoid automatic deployment on every push, providing additional control over the deployment process.

