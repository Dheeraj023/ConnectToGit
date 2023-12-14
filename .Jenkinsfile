pipeline {
    agent any
    // agent { docker { image 'python:3.12.1-alpine3.19' } }
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    stages {
         stage("Setup") {
            steps {
                script {
                    env.DOCKER_PLAYWRIGHT_NAME = "${env.BRANCH_NAME}".replaceAll('/', '-')
                    sh "(docker stop ${env.DOCKER_PLAYWRIGHT_NAME} && docker rm ${env.DOCKER_PLAYWRIGHT_NAME}) || true"
                    sh "docker run -d --name ${env.DOCKER_PLAYWRIGHT_NAME} -it --rm --ipc=host ${env.DOCKER_PLAYWRIGHT_IMAGE} /bin/bash"
                    sh "docker logs -f ${env.DOCKER_PLAYWRIGHT_NAME} &> docker.log &"
                    sh "docker exec -d -i ${env.DOCKER_PLAYWRIGHT_NAME} npm i playwright-firefox"
                    sh "docker exec -d -i ${env.DOCKER_PLAYWRIGHT_NAME} npx playwright install firefox"
                    sh "npm install"
                    sh 'npx playwright install'
                }
            }
        }
        stage('Variable Declaration in Jenkins') {
            steps {
                echo "${params.Greeting} World!"
            }
        }   
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
    }
    
}
