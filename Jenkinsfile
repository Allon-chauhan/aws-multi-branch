#!/usr/bin.env groovy

library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/Allon-chauhan/jenkins-shared-library.git',
    credentialsID: 'github-credentials'
    ]
)

pipeline {
    agent any
    tools {
            maven 'maven-3.9.9'
        }
    environment {
            IMAGE_NAME = 'nateallon/demo-app:jma-1.0'
        }

    stages {
        stage("build app") {
            steps {
                script {
                    echo "Building application jar..."
                    buildJar()
                }
            }
        }
        stage("build docker image") {
            steps {
                script {
                    echo "Building docker image..."
                    buildImage(env.IMAGE_NAME)
                    dockerLogin()
                    dockerPush(env.IMAGE_NAME)

                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    echo "Deploying the application..."

                    def shellCmd = "bash ./server-cmds.sh ${IMAGE_NAME}"

                    sshagent(['ec2-server-key']) {
                        sh "scp -o StrictHostKeyChecking=no server-cmds.sh ec2-user@54.80.169.215:/home/ec2-user"
                        sh "scp -o StrictHostKeyChecking=no docker-compose.yaml ec2-user@54.80.169.215:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@54.80.169.215 ${shellCmd}"
                    }
                }
            }
        }
    }
}