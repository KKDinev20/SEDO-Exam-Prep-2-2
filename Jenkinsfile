pipeline {
    agent any

    stages {
        stage('Checkout') {
            when {
                anyOf {
                    branch 'main'
                }
            }
            steps {
                checkout scm
            }
        }

        stage('Restore Dependencies') {
            when {
                anyOf {
                    branch 'main'
                }
            }
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                anyOf {
                    branch 'main'
                }
            }
            steps {
                sh 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            when {
                anyOf {
                    branch 'main'
                }
            }
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}