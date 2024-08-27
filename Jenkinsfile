pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                script {
                    // Clone the React app from GitHub
                    git url: 'https://github.com/rikka-maj123/reactjsawsload.git'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    // Navigate to the React app directory and build the app
                    dir('/home/jenkins/reactjsawsload') {
                        sh 'npm install'
                        sh 'npm run build'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Use SCP to copy the build files to the EC2 instance
                    sh 'scp -i /home/jenkins/reactprivate -r /home/jenkins/reactjsawsload/build/* ubuntu@13.229.67.88://home/ubuntu/'

                    // SSH into the EC2 instance to configure Nginx
                    sh '''
                    ssh -i /home/jenkins/reactprivate ubuntu@13.229.67.88 << EOF
                    sudo mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
                    echo "server {
                        listen 80;
                        server_name 13.229.67.88;

                        location / {
                            root /home/ubuntu;
                            index index.html index.htm;
                            try_files \$uri \$uri/ /index.html;
                        }
                    }" | sudo tee /etc/nginx/nginx.conf

                    sudo systemctl restart nginx
                    EOF
                    '''
                }
            }
        }
    }
}
