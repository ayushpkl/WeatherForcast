pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                // Installs packages if a package.json exists in your repo
                script {
                    sh '''
                        if [ -f package.json ]; then
                            npm install
                        else
                            echo "No package.json found, skipping npm install."
                        fi
                    '''
                }
            }
        }
        stage('Start Application') {
            steps {
                // Stop any previous running instance on port 3000 to prevent conflicts
                sh 'fuser -k 3000/tcp || true'
                
                // Run the Node.js application in the background using nohup
                // This ensures the app stays open and running after the Jenkins build finishes
                sh 'nohup node app2.js > app.log 2>&1 &'
            }
        }
    }
}
