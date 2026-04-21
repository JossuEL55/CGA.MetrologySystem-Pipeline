pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore CGA.MetrologySystem.slnx'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build CGA.MetrologySystem.slnx --configuration Release --no-restore'
            }
        }

        stage('Test') {
    steps {
        bat 'dotnet test CGA.MetrologySystem.slnx --no-build --configuration Release'
            }
        }  

        stage('Quality') {
            steps {
                echo 'Pending static analysis / code quality'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
        success {
            echo 'Build completed successfully.'
        }
        failure {
            echo 'Build failed. Review console output.'
        }
    }
}