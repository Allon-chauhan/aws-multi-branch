#!/usr/bin.env groovy

pipeline {
    agent any
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application..."

                }
            }
        }
        stage("build") {
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    echo "Deploying the application..."
                    def shellCmd = "bash ./server-cmds.sh"
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
