pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                // Clone the React app
                git url: 'https://github.com/rikka-maj123/reactjsawsload.git'
                
                // Clone the Angular app
                git url: 'https://github.com/rikka-maj123/angularawsload.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Build React app
                    dir('reactawsjenkins') {
                        sh 'npm install'
                        sh 'npm run build'
                    }
                    // Build Angular app
                    dir('angularawsload') {
                        sh 'npm install'
                        sh 'ng build --prod'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Use SSH to copy files to the EC2 instance
                    sh "scp -o StrictHostKeyChecking=no -r reactawsjenkins/build/* ubutnu@13.229.67.88:/var/www/react" // Replace with your EC2 public IP and path
                    sh "scp -o StrictHostKeyChecking=no -r angularawsload/dist/* ubuntu@13.229.67.88:/var/www/angular" // Replace with your EC2 public IP and path
                }
            }
        }
    }
}
