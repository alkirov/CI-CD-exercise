pipeline {
    agent any

    tools {
        nodejs 'NodeJS 24.4.1' // Ensure this name matches Jenkins configuration
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Start Application') {
            steps {
                bat 'start /b npm run start'
                sleep 5 // wait a few seconds to allow app to boot
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            bat 'taskkill /F /IM node.exe || exit 0'
        }
    }
}
