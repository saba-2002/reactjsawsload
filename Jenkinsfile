pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/rikka-maj123/reactjsawsload.git'
        DEPLOY_SERVER = 'ubuntu@13.229.67.88'
        DEPLOY_PATH = '/home/ubuntu/your-react-app'
        SSH_KEY = 'reactprivate'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: "https://github.com/rikka-maj123/reactjsawsload.git"
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['react-deploy-ssh-key']) {
                    sh "ssh -i ~/.ssh/${SSH_KEY} ${DEPLOY_SERVER} 'mkdir -p ${DEPLOY_PATH}'"
                    sh "scp -i ~/.ssh/${SSH_KEY} -r build/* ${DEPLOY_SERVER}:${DEPLOY_PATH}"
                }
            }
        }
    }
}
