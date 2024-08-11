pipeline {
    agent any

    environment {
        EC2_IP = '18.171.184.51'
    }

    /*stages {
        stage ('fetch code') {
            steps {
                script {
                    echo "Pull source code from Git"
                    git credentialsId: 'Git', branch: 'deploytoec2', url: 'https://github.com/seunayolu/deploytoec2.git'
                }
            }
        }*/
        
        stage ('deploy to EC2') {
            steps {
                script {
                    echo "deploying to shell-script to ec2"
                    def shellCmd = "bash ./websetup.sh"
                    sshagent (['EC2']) {
                        sh "scp -o StrictHostKeyChecking=no websetup.sh ubuntu@${EC2_IP}:/home/ubuntu"
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@${EC2_IP} ${shellCmd}"
                    }
                }
            }
        }
    }
}