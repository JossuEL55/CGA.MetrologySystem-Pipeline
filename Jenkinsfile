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
                bat 'scripts/restore.bat'
            }
        }

        stage('Build') {
            steps {
                bat 'scripts/build.bat'
            }
        }

        stage('Validation') {
            parallel {
                stage('Test') {
                    steps {
                        bat 'scripts/test.bat'
                    }
                }

                stage('Quality') {
                    steps {
                        bat 'scripts/quality.bat'
                    }
                }
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