pipeline {
    agent any

    tools {
        nodejs 'NodeJS 24.4.1'
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
                sh 'nohup npm run start &'
                sleep 5 // Give the app time to start
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
            sh 'pkill node || true'
        }
    }
}
