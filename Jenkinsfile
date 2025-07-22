pipeline {
    agent any

    tools {
        nodejs 'NodeJS 18.X' // Make sure this matches the configured name in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Start Application') {
            steps {
                sh 'npm run start &'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'pkill node || true' // Clean up the app if it was started
        }
    }
}
