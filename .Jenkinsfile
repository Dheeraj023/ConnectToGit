pipeline {
  agent none
  tools{
        dockerTool 'DockerContainer'
  }
  stages {
  	stage('Maven Install') {
    	agent {
      	docker {
        	image 'maven:3.5.0'
        }
      }
      steps {
      	sh 'mvn clean install'
      }
    }
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t shanem/spring-petclinic:latest .'
      }
    }
  }
}
/* pipeline {
    agent any
    // agent { docker { image 'python:3.12.1-alpine3.19' } }
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    tools{
        DockerContainer 'docker'
    }
    stages {
       stage('Variable Declaration in Jenkins') {
            steps {
                echo "${params.Greeting} World!"
            }
        }   
        stage('build') {
            steps {
                // sh 'python --version'
                echo "docker tool implementation"
            }
        }
    }
    
}*/
