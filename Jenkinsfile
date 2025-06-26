pipeline {
    agent any

    environment {
        DOTNET_ROOT = "${env.USERPROFILE}\\dotnet"
        PATH = "${env.USERPROFILE}\\dotnet;${env.PATH}"
    }

    stages {
        stage('Install .NET 6 SDK') {
            steps {
                bat 'powershell -Command "Invoke-WebRequest https://dot.net/v1/dotnet-install.ps1 -OutFile dotnet-install.ps1"'
                bat 'powershell -ExecutionPolicy Bypass -File .\\dotnet-install.ps1 -Version 6.0.421 -InstallDir %USERPROFILE%\\dotnet'
            }
        }

        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
