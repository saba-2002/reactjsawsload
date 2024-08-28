pipeline {
    agent any

    stages {
        stage('Clone React App') {
            steps {
                git 'https://github.com/rikka-maj123/reactjsawsload.git'
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
                sh 'rsync -avz -e "ssh -i /home/jenkins/.ssh/id_rsa" /var/lib/jenkins/workspace/react-app/build/ ubuntu@18.141.185.119:/var/www/html/react'
            }
        }
    }
}
