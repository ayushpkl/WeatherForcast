pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Start Web Server') {
            steps {
                // Stop any existing Python web server running on port 8000
                sh 'pkill -f "http.server 8000" || true'
                
                // Start a detached static web server on port 8000 so Jenkins does not kill it
                sh 'JENKINS_NODE_COOKIE=dontKillMe nohup python3 -m http.server 8000 > server.log 2>&1 &'
            }
        }
    }
}
