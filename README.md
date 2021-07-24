## Instructions for Deployment

### build command

`docker build -t scatest:latest .`

### Command to run the container

`docker run -d -p 8000:80 scatest:latest`

### Command to push docker image to docker hub

`docker push scatest:latest`

[Docker Hub Link](https://hub.docker.com/repository/docker/maryjaneak/scatest)

### Jenkins Pipeline Syntax

<p><b>Jenkins Pipeline </b> represents a user-defined model of a continuous deployment pipeline. A Pipeline’s code defines the entire build process, which includes stages of building, testing and deploying the application, </p>

<p><b>A stage block</b> defines a conceptually distinct subset of tasks performed through the entire pipeline</p>
<p></b>A step</b> represents a single task involved in a stage block</p>

- A Jenkinsfile with declarative pipeline syntax

```pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                //
            }
        }
        stage('Test') {
            steps {
                //
            }
        }
        stage('Deploy') {
            steps {
                //
            }
        }
    }
}





```

- A Jenkinsfile with a scripted pipeline syntax

```node {  
    stage('Build') { 
        // 
    }
    stage('Test') { 
        // 
    }
    stage('Deploy') { 
        // 
    }
}


```

- An example of a Jenkinsfile with a scripted pipeline syntax

```pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                sh 'make' 
            }
        }
        stage('Test'){
            steps {
                sh 'make check'
                junit 'reports/**/*.xml' 
            }
        }
        stage('Deploy') {
            steps {
                sh 'make publish'
            }
        }
    }
}


```
- An  example of a Jenkinsfile with a scripted pipeline syntax

```node { 
    stage('Build') { 
        sh 'make' 
    }
    stage('Test') {
        sh 'make check'
        junit 'reports/**/*.xml' 
    }
    if (currentBuild.currentResult == 'SUCCESS') {
        stage('Deploy') {
            sh 'make publish'
        }
    }
}

```

-	agent is declarative Pipeline-specific syntax that instructs Jenkins to allocate an executor (on a node) and workspace for the entire Pipeline.
- sh is a  step provided by the Pipeline: Nodes and Processes plugin that executes the given shell command.
- junit is provided by the JUnit plugin for aggregating test reports.
- node is scripted pipeline-specific syntax that instructs Jenkins to execute this Pipeline (and any stages contained within it), on any available agent/node. 

