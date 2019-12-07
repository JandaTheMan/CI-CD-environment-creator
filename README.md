# CI-CD-environment-creator
CI-CD-environment creator is a set of pieces that handles the creation, startup and configuration 
of the necessary components to get a ready infrastructure for a broad range of projects. 
With this environment the teams will be able to develop its projects following the principles 
that make the Continuous Integration most effective getting the Continuous Delivery approach.


## Modules
**Infrastructure module:**

The infrastructure module will have the capability to create, startup and manage the necessary environment where build and deploy 
all code changes pushed to the projects mainline in an automated way. 

[Infrastructure Creator](https://www.github.com.com/JandaTheMan/infrastrucutre-creator.git)

**Pipelines module**

Pipelines module will provide to create pipelines for the projects to be executed on the environment created by the 
infrastructure module. 

[Jenkins Pipelines Library](https://www.github.com.com/JandaTheMan/jenkins-pipelines-library.git)

---

***The next sections are a theoretical exposure of key concepts of Continuous Integration and Continuous Delivery to justify 
the components used in this project as well as the benefits of adopting such platform for the development teams. There are presented a lot of 
basic concepts of the CI and CD methodologies and of the tools used in the project.*** 

***The modules usage are explained in the README of each one.***


***Only keep reading if you want to get a deeper knowledge about the motivations of the project and a brief exposition about Continuous Integration and Continuous Delivery/Deployment.***

## Introduction

In Traditional software development, it was common for developers to work isolated for a long time, merging the resulting code after that. 
This practice had a bad consequence: it could take days or even weeks for software developers to integrate their code and also merge changes from the different version of each developer. 
These isolated developments produced, in addition to merge conflicts, code strategy divergence and duplicated effort.
As a result, it was difficult to provide code updates quickly. The feedback about the developed changes was not immediate but after the code merge, being more likely to find bugs due to the code isolation. 
It is worth to mention that isolated code bugs combined together, could create more code problems.

## Continuous Integration / Continuous Delivery (CI/CD)

According to Wikipedia [1], Continuous Integration (CI) in software engineering is the practice of merging all developer's working copies to a shared mainline several times a day. With this definition it can be seen that CI entails a cultural component, as developers have to learn to integrate code periodically.

**The main goal of CI is to reduce the time to feedback over the software integration process, allowing to locating and fixing bugs more easily and quickly, thus enhancing its quality while reducing the time to validate and publish new software updates.**

This means that, by following the CI culture, a team of developers can avoid the traditional problems of the merge and integration of the isolated parts of the code, getting a stable version of the developing software always ready.
CI, on the other hand, entails an automation component. From the culture of CI, as a consequence, principles, practices and processes that automate and carry out the methodology are born.

Martin Fowler wrote in his blog [2] an article about the key principles that make CI effective. Those principles are:

* 'Maintain a Single Source Repository'

* 'Automate the build'

* 'Make your build self-testing'

* 'Everyone commits to the mainline everyday'

* 'Every commit should build the mainline on the integration machine'

* 'Fix broken builds immediately'

* 'Keep the build fast'

* 'Test in a clone of the production environment'

* 'Make it easy for anyone to get the latest executable'

* 'Everyone can see what is happening'

So far, the need for adopting CI in a project has been explained. The basic CI definition, that entails a cultural component, triggers, as a consequence, a set of principles that involve some practices and automation processes and tooling.
This process does not explicitly include the deployment to the production-like environment.

Traditional software deployment involved IT operation teams in charge of the deployment process. This resulted as a wall between development and operations. IT teams responsible of the deployment often had other things they were working on in parallel.
So, the deployment schedule was determined by when they were available, preventing them to meet the business needs. Adopting CI means getting a healthy mainline, with all the benefits from getting rapid feedback about the code to improve its quality, becoming ready to be deployed when the business needs it.
This is strongly related with agile methodologies of releasing small pieces of useful functionalities.

In that context, Continuous Delivery and Continuous Deployment are two software slightly different approaches that automate the software deployment and let the team focus on building the product, being agnostic of the deployment process stage in the software development.
The incremental and continuous builds offered by adopting CI are translated as continuous deployments with the CD approaches.

These two approaches are often interchanged, but they are not the same. Continuous Delivery automates the deployment of the software on a regular basis to a production-like environment.
This mean that the latest stable version is deployed automatically to all test environments that the enterprise has available, replicating or mimicking the production environment as much as possible.
The final objective is to ensure that the software can be deployed at any time, simply by clicking the deploy button. It is worth to mention that the deployment process is tested in the test environments each time a deployment is performed, so there is a strong confidence about the process.
The continuous Deployment is almost the same but with one significant difference: the production environment deployment is also automatic when the tests in all production- like environments pass successfully.
That is, no human interaction exists after the code commit that triggers the deployment process.

The CD approach is modelled by the delivery Pipeline, where automated builds, tests and deployments are orchestrated as one release workflow. The delivery pipeline is a set of steps that code changes will go through until ready to be deployed to production. 
The steps that are grouped in pipeline stages are defined by the software constraints and the business needs



## Decision of technologies used in the project 

To be compliant with the Martin Fowler's principles, the main tools the project need were:

* A source control manager: to maintain a single source repository and get a method to ensure that every commit build on the integration machine.

* A CI server: to build automatically (and pass the project tests) every commit on the integration machine. The server will orchestrate the deployment in the desired environments. Its function extends to show the state of the project pipelines, so that everyone can see what is happening.

+ A virtualization tool to easily replicate the environment in the production-like environments, as well as in the development machine.

* An artefact storage system to make it easy for anyone to get the latest executable.

The creation of the infrastructure will be done by the project modules: the project consumers only has to fill a configuration file and the system will generate all the necessary stuff. To accomplish this specification, a tool that performs the creation and setup of a cloud system instances is needed.

With these specifications in mind, the tools used in this project will be presented in the next sections.
 ### Source Control Manager
The technology behind the source control manager is git. Git is a widely extended open source version control manager. Its purpose is to track changes in any set of files, designed for coordinating work among programmers.


The usage of git is very simple: the end-user can download the source code, placed in a remote git repository (it is worth to mention that the tool can also be used locally, so that the user can initialize a project in the computer and get the benefits of the tool). Once downloaded, there is a broad range of different information that git can extract 
about the downloaded project, or actions to do on the project code. The most used of these possibilities that can help in the good practice of the CI are:

* Showing the historic of the code changes. CI fosters a strong communication. So, related to the communication with the developer team, one can see the changes that the teammates have done. Each developer set of changes are submitted to the code through git commits. These commits are accompanied with a message that should summarize the changes, hence existing an explicit communication.

* One can revert the state of the project to the state of specific git commit. If some pushed commit to the mainline breaks the build, the developers can rapidly revert the last pushed commit to the state previous of the break and try to fix it before pushing it to the mainline again.

* When merging the code state with the mainline, git alerts and shows any integration conflict that may exist. When following the CI culture, the integration with other developers is key. Git makes this easier by telling where the integration conflicts exists thus making the integration more comfortable.

https://git-scm.com/
### CI Server

Currently there are many CI server solutions to consider when creating a CI/CD system and a great part of them are open source projects. Its common usage is to define the pipeline stages and its steps in a configuration file with its domain specific language, whatever it is for that server.
The CI server chosen for this project is Jenkins. Currently, Jenkins is one of the most extended CI servers and it has a lot of plugins for the interoperability with a broad range of technologies.

The way to create pipelines in Jenkins is through the Jenkinsfile. In this file, a pipeline is modelled by the Jenkinsfile domain specific language, based in groovy. This domain specific language has native support to call shell scripts in Linux and Windows systems, source control manager tools or notification support via email among others, with the advantage that one can program the flow as in a groovy script.

https://jenkins.io/

### Virtualization Tool

Replicate the production environment is desired to execute the tests in the same conditions as in which the software project will be executed on.

Docker is a tool that provides an abstraction layer of the Linux Containers that automates the virtualization of an application in multiple operating systems.
In a nutshell, this technology creates an isolated system into the host machine, sharing the kernel resources.
It looks like a virtual machine but faster, with a better portability and more lightweight: it is a software virtualization instead of hardware virtualization. 

These isolated environments inside the host machine are called containers, and these containers are modelled by the docker images.
A container is an initialized instance of an image. Each image contains the information about the system to create. The images are created from Dockerfiles, whose description defines the final container ecosystem.

The Dockerfile description allows a huge number of configurations, such as system type (Windows or Linux), environment variables, commands to execute in the start-up of the container, and a large etcetera.
The last description in the Dockerfile is the command to execute when the container starts, and the lifecycle of this container ends when the command executed ends.
To run our desired code inside a docker container, after describing the environment, we have to copy the build code in the container.
The way to describe Dockerfiles is designed for this. At the end of the description, we must specify the main entry point of the application.

The replication of the production environment now is only a simple copy of the configuration file of the production environment (Dockerfile) with possible little changes.
The resulting image will become the artefact to deploy on the production-like and production machines. 

https://www.docker.com/

### Artefacts Storage
The artefacts storage role is to provide access to everybody to get the latest build completed successfully, which will be stored in that repository.
In addition, the development team gets a way to deploy the version they need.

In the situation when some bug is not detected by tests and the code gets deployed in production, the team need to roll back to the last stable version.
This procedure is easily accomplished getting the last stable build and deploying it to the production. Once the virtualization technology chosen is Docker, and the deploy artefacts are docker images, the artefacts repository chosen for the project will be the Docker Registry.

Docker registry is a hosting repository to push and pull images from. It can be easily used only running the Docker Registry image in the desired Docker Host.
Each build will push the created image referenced by a version to the registry, and the deployment machine will pull these images from the registry to start the deployment.

https://docs.docker.com/registry/

### Cloud Services Handler

To start working with the CI/CD platform, there exists some initial automated configuration: the CI-CD environment creator in this project is in charge of starting and configuring the integration machine and the deploy one and orchestrate its connection. 
In addition, the project should be adaptable as many cloud technologies as possible.

Terraform is the tool that can handle these requirements. It allows provisioning and managing a lot of cloud providers, infrastructures or services.
With this, the start-up and management of the cloud instances can be done programmatically with the Terraform domain specific language.
To setup the machines, the main task is to create system scripts to configure all instance requirements that will be provisioned and executed on the desired instances. 
  
   
 https://www.terraform.io/


## Bibliography

[1] "Continuous Integration". Wikipedia [Online] Available https://martinfowler.com/articles/continuousIntegration.html

[2] Martin Fowler. "Continuous Integration". Martin Fowler blog [Online] Available: https://martinfowler.com/articles/continuousIntegration.html 