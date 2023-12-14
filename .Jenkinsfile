pipeline {
    // agent any
    agent { docker { image 'python:3.12.1-alpine3.19' } }
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    tools{
        docker 'DockerContainer'
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
    
}
