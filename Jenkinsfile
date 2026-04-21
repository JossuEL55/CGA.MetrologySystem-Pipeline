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
    }
}