pipeline {
    agent any

    stages {
        stage('Clone React App') {
            steps {
                git 'https://github.com/saba-2002/reactjsawsload.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy React App') {
            steps {
                sh 'rsync -avz -e "ssh -i /home/jenkins/id_rsa" /var/lib/jenkins/workspace/reactapp/build/ ubuntu@10.0.2.28:/var/www/html/react'
            }
        }
    }
}
