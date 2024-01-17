pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "C:\\Program Files\\dotnet"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Restoring dependencies
                    bat "cd ${DOTNET_CLI_HOME} && dotnet restore"

                    // Building the application
                    bat "cd ${DOTNET_CLI_HOME} && dotnet build --configuration Release"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Running tests
                    bat "cd ${DOTNET_CLI_HOME} && dotnet test --no-restore --configuration Release"
                }
            }
        }

        stage('Publish') {
            steps {
                script {
                    // Publishing the application
                    bat "cd ${DOTNET_CLI_HOME} && dotnet publish --no-restore --configuration Release --output .\\publish"
                }
            }
        }
    }

    post {
        success {
            echo 'Build, test, and publish successful!'
        }
    }
}
