# Devsecops

- How the software development lifecycle can be optimized with fail early and fail fast.

## Who am i

- I love to code many of automation scripts.
  ...

## CI/CD Pipeline

1- developers commits the code.
2- dependencies are fetched and project is built.
3- use hardened image and deploy product over it.

- Code commit < Build < Deploy
- Continuous Integration = Code commit + Build
- Continuous Deployment = Deploy

## Devops and SDLC

1- [collaborate]:

- Jira
- trello
- slack
- Microsoft Teams

2- [Build] :

- SCM/VCS (source controle management) = Git, Gitlab, Bitbucket.
- CI = Jenkins
- Build = Gradle, Maven
- DataBase management = DBDeploy, DBmaestro

3- [TEST] :

- JUNIT
- JMeter
- Pytest
- BlazeMeter
- Selenium

4- [DEPLOY] :

- Docker
- Ansible
- Vagrant
- Chef
- Terraform

5- [RUN] :

- Cloud = Amazon, GCP, OpenStack, CloudFoundry.
- Orchestration and scheduling = kubernetes, docker swarm, meosphere, mesos, nomad.

## What needs to be understood ?

- selection of tools
- opportunity to automate
- metrics is important
- false positives need manual analysis
- Tools can't replace PENTESTING!

## Basic CI/CD Pipeline

- whenever there is a commit
- it triggers a tool (Jenkins) that runs all automation build steps.
  - build the container
  - functional test cases
  - UI test cases
- if build success, the jenkins will create an artifact and store it.
  - artifact = the final build that will be consumed by consumer;
- Deployed to production environment.

## What we will do ?

- in CI/CD pipeline add security checks :

  - check commits for sensitive info
  - build the container/product
  - host vulnerability assessment on OS where product is goingn to be hosted.
  - source composition analysis ( identify vulnerabilities from third-parties apps)
  - static application security testing
  - dynamic application security testing (try to attack app from outside)
  - container security testing.

  --> vulnerabilities will be notified in a Vulnerability Management Tool ( Defect Dojo ).

## Setting up Jenkins Server

- ssh to jenkins
- install java
- install jenkins
- install docker
- modify rule in Security Groups for port 8080
- Activate Jenkins from /var/lib/Jenkins/secrets/initialAdminPassword

### ---------------------- INTERVIEW QUESTIONS

## 1- elaborate on devsecops

- making everyone responsible for security, with the aim of implementing security choices and actions at a similar pace and scale as those of dev and operations.

## 2- How does configuration management fit into devops ?

- allows for management of different systems and changes to them
- preserve integrity of the overall infrastructure.

## 3- How devops increase systems security ?

- through VM images or scanning containers for defined software flaws,
- rejecting builds that include problematic packages,
- execute static analysis tools;

## 4- what is devops ?

- a method of software development that allows teams to build, test, and deliver software more quickly and reliably.

## 5- devops lifecycle :

- conception
- design
- maintenance
- development
- test
- release
- support

= Plan < code < Build < build < test < release < deploye < operate monitor < plan

## 6- Tools for pentesting:

- kali linux
- nmap = network mapper, used for port scanning, and find vulnerabilities in ports.
- metasploit = penetration testing framework
- wireshark = network protocol analyzer, tool to understand the traffic passing accross your network.
- JohnTheRipper = used to crack encryption.
- Burp Suit = Web vulnerability scanner.
