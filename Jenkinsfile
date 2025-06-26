pipeline {
    agent any

    stages {
        stage('Install .NET 6 SDK') {
            steps {
                bat 'powershell -Command "Invoke-WebRequest https://dot.net/v1/dotnet-install.ps1 -OutFile dotnet-install.ps1"'
                bat 'powershell -File .\\dotnet-install.ps1 -Version 6.0.421 -InstallDir %USERPROFILE%\\dotnet'
            }
        }

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
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                anyOf {
                    branch 'main'
                }
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            when {
                anyOf {
                    branch 'main'
                }
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}