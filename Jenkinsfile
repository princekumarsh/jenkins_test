pipeline {
    agent { label 'agent_237' } // Specify the label of your AWS agent
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/princekumarsh/jenkins_test.git' // Replace with your GitHub repository URL
            }
        }

        stage('Upload to AWS Agent') {
            steps {
                sh 'scp -i /home/princekumar/Downloads/test-key-pair.pem -r * ubuntu@13.201.47.237:/usr/share/nginx/html' // Replace with your AWS agent IP and destination path
            }
        }

        stage('Deploy with Nginx') {
            steps {
                sh 'ssh -i /home/princekumar/Downloads/test-key-pair.pem ubuntu@13.201.47.237 "sudo systemctl restart nginx"' // Restart Nginx or perform any other deployment tasks
            }
        }
    }
}
