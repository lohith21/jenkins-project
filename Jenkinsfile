pipeline {
    agent any
    environment {
        SERVER_IP = credentials('k8s-worker2')
    }
    stages{ 
     stage('Setup') {
            steps {
                sh "pip install -r requirements.txt"
            }
       }
     stage('Test'){
            steps{
                sh "pytest"
            }
        }
     
     stage('Package code') {
        steps {
            sh "zip -r myapp.zip ./* -x '*.git*'"
            sh "ls -lart"
        }
     }

     stage('Deploy to Prod') {
        steps {
            withCredentials([sshUserPrivateKey(credentialsId: 'k8s-worker2-key', keyFileVariable: 'MY_SSH_KEY', usernameVariable: 'username')]) {
                sh '''
                scp -i $MY_SSH_KEY -o StrictHostKeyChecking=no myapp.zip ${username}@${SERVER_IP}:/home/vagrant/
                ssh -i $MY_SSH_KEY -o StrictHostKeyChecking=no ${username}@${SERVER_IP} <<EOF
                     unzip -o /home/vagrant/myapp.zip -d /home/vagrant/app/
                     pwd
                     cd /home/vagrant/app/
                     pwd
                     source app/venv/bin/activate
                     pip install -r requirements.txt
                     sudo systemctl restart flaskapp.service
                EOF
                 '''
            }
        }
     }

    }
}
