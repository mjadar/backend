# GITLAB CI/CD

## Benefits of Gitlab CI/CD

- seamless integration into code repository
- using CI/CD without overhead of setting it up yourself
- Pipeline configuration as part of your application code.
- self hosted or paas.

## Negative points for other tools (JENKINS)

- provides only ci/cd tool
- self hosting is the only option

## Gitlab Architecture

- `Gitlab server` hosts your application code and pipelines.
- so it manages the pipeline configuration
- and then there are multiple `gitlab runners`, separate machines connected to gitlab server machine, and these one executes the pipeline.

## How to create your pipeline

- pipeline is written in code
- hosted in the app git repo itself in yaml file, called `.gitlab-ci.yml`
- [tasks] such as run tests, build image, deploy to server, etc are configured as jobs;
- [Jobs] are the most fundamental building block of a .gitlab-ci.yml; Jobs define what to do;

- on gitlab an execution environment is DOcker container, so instead of executing directly on the OS. We execute the jobs on the containers.
- Gitlab runner creates docker containers to run the jobs.
- Gitlab's managed runners are using Ruby image to start the container.
- Variable definition can be done in job level or in pipeline level, it depends on the scope where we want to use our variables.

## Example

### Step 1 ==> Run_tests job

- for jobs to be executed successfully our example needs make, pip, python to be available on the machine where our program will run.
- Gitlab's managed runners use Ruby image, but we need Python not Ruby.
- `Before_script` = are commands that should run before script command. used to prepare environments, fetch data, create tmp files.
- After_scrip = used to define commands that run after each job, including failed jobs.

- Our pipeline :
  - Run tests
  - Build docker image
  - Push to Docker Registry
  - Deploy to server

```JOB1 RUN_TESTS
run_tests:
    image: python:3.9-slim-buster
    before_script:
        - apt-get update && apt-get install make
    script:
        - make test
```

### Step 2 ==> Build and push docker image

- First, we will add a second job in the pipeline we defined.
- For that, we need credentials of our docker repository (username and password), we will not hard code them in the YAML file but in secret variables that we will define under `Settings->CI/CD->Variables`.
- Project Variables are stored outside the git repository (not in the .gitlab-ci.yml); Ideal for tokens and passwords, which should not be included in the repository for security reasons!

- Second, we want to build a Docker image from a Dockerfile.
- `docker build -t REPOSITORY .` = the repository location is included in the image name, so that later when we execute the push command it knows where it will be pushed; The point is the location of the Dockerfile.

- We need docker to be available inside the docker container, `Docker in Docker`

- [REMINDER] = `Docker build `is used to build DOcker images from a Dockerfile.

- we need also a docker daemon available inside our container. Docker daemon is the process that lets the clients execute the commands to connect to docker registry, pull/push image etc... ; So to make this available, we need to configure another attribute called `service`.
- [service] = additional container that starts at the same time as job container, and the job container can use this service at build time.
- so recap, in the build_image job we define the container in image, and the service container under service. And to make sure these two can communicate with each other they need to have the same certificate. We do that by defining a variable
  `DOCKER_TLS_CERTDIR: "/certs" `

```JOB2 BUILD and PUSH docker images
build_image:
    variables:
        IMAGE_NAME: mjadar/demo-app
        IMAGE_TAG: python-app-1.0
    image: docker:20.10.16
    services:
        - docker:20.10.16-dind
    variables:
        DOCKER_TLS_CERTDIR: "/certs"
    before_script:
        - docker login -u $REGISTRY_USER -p $REGISTRY_PASS
    scripts:
        - docker build $IMAGE_NAME:$IMAGE_TAG .
        - docker push $IMAGE_NAME:$IMAGE_TAG
```

## Define stages

- the issue is both stages are executed at the same time, but we want to run them in order.
- Only if the tests are successful, we want to build the Docker image.
- And only if build and push was successful, we want to deploy that new image.
- We can achieve this using `stages`; We can group multiple jobs into stages, that run in a defined order.

- in our example, we have 2 jobs, `run_tests` and `build_image`.
- so we define `stages` attribute

```
variables:
        IMAGE_NAME: mjadar/demo-app
        IMAGE_TAG: python-app-1.0

stages:
    - test
    - build

run_tests:
    stage: test
    image: python:3.9-slim-buster
    before_script:
        - apt-get update && apt-get install make
    script:
        - make test

build_image:
    stage: build
    image: docker:20.10.16
    services:
        - docker:20.10.16-dind
    variables:
        DOCKER_TLS_CERTDIR: "/certs"
    before_script:
        - docker login -u $REGISTRY_USER -p $REGISTRY_PASS
    scripts:
        - docker build $IMAGE_NAME:$IMAGE_TAG .
        - docker push $IMAGE_NAME:$IMAGE_TAG
```

## Step 3 Deploy to server job

1- Gitlab's Runner needs to SSH into the deployment server

- '-d' flag = run in detached mode, otherwise it will block our terminal for other jobs.
- add before script to change permission to the tmp file created, cuz Gitlab give automatically read write permission to everyone.
- kill and remove all docker containers before you run, cuz it can say that the port is already taken when starting the given container.

```
deploy:
    stage: deploy
    before_script:
        -  chmod 400 $SSH_KEY
    script:
        - ssh -o StrictHostKeyChecking=no -i $SSH_KEY root@IP_ADDRESS "
            docker login -u $REGISTRY_USER -p $REGISTRY_PASS &&
            docker ps -aq | xargs docker stop | xargs docker rm &&
            docker run -d -p 5000:5000 $IMAGE_NAME:$IMAGE_TAG
        "
```

## Bonus

- By default Gitlab create temp files with read write permission to everyone.
- ssh -i private_key root@IP_ADDRESS
