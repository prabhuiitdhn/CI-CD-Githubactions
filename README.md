### CI/CD using github actions.

Github actions: CI/CD platform one of the workflow where github actions automate developer workflows; It basically helps to automate the process as much as possible.

![image](https://github.com/prabhuiitdhn/CI-CD-Githubactions/assets/19517005/cecb8f1f-87bb-4a6f-b877-54976af5441c)


The cost of using MLOps pipeline tool and automation tool are bit costly which does not help return the benefits, So, using Github action is another solution to make the pipeline.

GitHub Actions is a tool offered by GitHub built to automate software workflows. For instance, software developers use GitHub Actions to automate branch merges, for handling issues in GitHub, doing application tests, etc.
Github actions is not parallelizable.

However, we as Data Scientists can also use GitHub Actions for many things which will use it for automate several steps of the MLOps flow
    - Automating the ETL process.
    - Checking whether the model should be retrained or not.
    - Uploading the new model to your cloud provider and deploying it.

To work with Github actions, we just need to add a .yaml file into .github/workflows
in .yaml file, we specify
    - the name of the workflow
    - When should the workflow trigger: based on a cron schedule, http request, manually, etc.
    - The OS where the workflow will run (Ubuntu, Windows or MAC).
    - Each of the steps that the workflow should execute.

Pros and cons of using GitHub Actions as MLOps workflows:
    - Easy to use
    - GitHub Actions works with the main programming languages used for Data Science: Python, R, Julia, etc.
    - You can use the experience of learning GitHub Actions to automate other processes.
    - GitHub Actions is free for public repositories.
    - This automation works perfectly with main Cloud providers such as AWS, Azure and Google Cloud,
    - Every time a workflow fails you will automatically receive an email.

cons:
    - You have many models that you must put into production or a few but complex models (such as Deep Learning models). In this case, you will need a lot of computing power to train your models and GitHub Action’s machines are not suited for that.
    - You are already using a tool that could be used for MLOps. For example, imagine that you are using Apache Airflow for ETL processes. In that case, it probably would be a better idea to use this tool for MLOps rather than building an MLOps pipeline with GitHub.


Github Events: when github workflows needed to check and build again and ask for pull request is called as event.

Workflows: merged code -> test-> build -> deployment[Update the version number]

Actions: Sorting the actions, label, assign it, and reproduce the actions are the gihub actions

CI/CD with Github actions
- commit code, test the code, build the code, push the code and deploy the code in deployment server.
- if code is being hosted through github then no need to use third party integration tool. Github action can be use for CI/CD pipleline
- setup the pipeline is easy

syntax of workflow
```

name: # It is name of the workflow
on: #This is for event
    push: # this is in the case of piushing the code into master branch
        branches: [Master]
    pull_request: # this is in the case of if someone ask for pull request for the code/ github repo
        branches: [Master]

jobs: # this show what are the jobs will be done when workflow starts
    build: # this show start the building the repo
        runs-on: ${{matrix.os}} # this says that start building on ubuntu:latest os
        strategy:
            matrix:
                os: [ubuntu-latest, windows-latest, macOS-latest]

        steps: # shows the steps needs to be followed< It can run commands, setup tasks, or run the action
        -uses: actions/checkout@v2 # It is basically said checkout the repo which is in gihub main branch
                                   # so basically we can se actions in gihub/actions and check what does checkout do?
                                   # they will have .yaml file which supports actions using checkout
                                   # https://github.com/actions/checkout/blob/main/action.yml
                                   # https://github.com/iterative/cml#github
                                   # v2: version of the action

        -name: Generate metrics report # Name of the actions
        -uses: actions/setup-something # it uses this actions
        with:
         python-version: 3.8 # It basically says build with action setup-something with python 3.8 version
        env: # what enviroment we want to have it.
            REPO_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run:
            # Add the command we want to work on it, Linux command; below given command will start working on it.
            pip install requirement.txt
            python train.py
```

to find any action which might be available in github market place
Like to push and pull docker image into docker hub.
[docker push and pull action+github+marketplace] helps to give this links
https://github.com/marketplace/actions/docker-build-push-action
THis below actions provide uses for docker build push action
It basically tell which docker hub id, username pass and repo name and all
steps:
  - uses: actions/checkout@v3
    name: Check out code

  - uses: mr-smithers-excellent/docker-build-push@v6
    name: Build & push Docker image
    with:
      image: prabhuiitdhn/test_po //this account is created into docker hub; This is repo/image name
      tags: v1, latest # what tags of dccker image we need.
      registry: registry-url.io
      dockerfile: Dockerfile.ci # this is reference of giving docker file
      username: ${{ secrets.DOCKER_USERNAME }} #this is docker username & password. Also, it can be added in github secret.
      password: ${{ secrets.DOCKER_PASSWORD }}

Where github actions runs?
    - github server and managed by server
    - for each job, new or fresh github server created and used to execute the jobs
    - github server make available system as required os like ubuntu, mac or windows os system which mentions on runs-on.

Example:
https://www.youtube.com/watch?v=9BgIDqAzfuA&t=417s&ab_channel=DVCorg

Example:
    https://neptune.ai/blog/build-mlops-pipelines-with-github-actions-guide
    https://neptune.ai/blog/mlops-tools-platforms-landscape
 - Build a MLOps pipelines with github and Google cloud
 - Build a MLOPs pipeline and putit into production with github, github actions, and google cloud.
 - model is no of bitcoin transations per hour.
 Learning
  - How to set up data extraction pipelines with GitHub Actions.
  - How to build a model-train and selection pipeline with GitHub Actions.
  - How to wrap your model as an API.
  - How to Dockerize your API so that your code is portable and deployable in any Docker-friendly cloud service.
  - How to set up a continuous deployment pipeline with Cloud and GitHub Actions.
  - How to automate model retrain with GitHub Actions.

Important Links.
https://www.youtube.com/watch?v=R8_veQiYBjI&ab_channel=TechWorldwithNana
https://docs.github.com/en/actions/quickstart
https://docs.github.com/en/actions/deployment/about-deployments/deploying-with-github-actions
https://github.com/actions/checkout/blob/main/action.yml
https://github.com/iterative/cml#github

https://anderfernandez.com/en/blog/github-actions-for-data-science/
