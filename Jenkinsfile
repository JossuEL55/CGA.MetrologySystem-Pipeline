def restoreSolution() {
    bat 'dotnet restore CGA.MetrologySystem.slnx'
}

def buildSolution() {
    bat 'dotnet build CGA.MetrologySystem.slnx --configuration Release --no-restore'
}

def runTests() {
    bat 'dotnet test CGA.MetrologySystem.slnx --no-build --configuration Release'
}

def runQualityCheck() {
    bat 'dotnet format CGA.MetrologySystem.slnx --verify-no-changes'
}

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
                script {
                    restoreSolution()
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    buildSolution()
                }
            }
        }

        stage('Validation') {
            parallel {
                stage('Test') {
                    steps {
                        script {
                            runTests()
                        }
                    }
                }

                stage('Quality') {
                    steps {
                        script {
                            runQualityCheck()
                        }
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