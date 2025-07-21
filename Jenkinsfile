pipeline {
    agent any

    environment {
        NODE_ENV = 'development'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Set Up Node.js') {
            steps {
                echo 'Setting up Node.js...'
                // Assumes NodeJS plugin is installed in Jenkins
                // Replace 'NodeJS 18' with your configured Node version name
                tool name: 'NodeJS 18', type: 'nodejs'
                script {
                    env.PATH = "${tool 'NodeJS 18'}/bin:${env.PATH}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing npm packages...'
                sh 'npm ci'
            }
        }

        stage('Start Application') {
            steps {
                echo 'Starting application...'
                sh 'nohup npm start &'
                // optional wait to ensure server is up
                sh 'sleep 3'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Kill any node process if needed (optional)
            sh 'pkill node || true'
        }
    }
}
