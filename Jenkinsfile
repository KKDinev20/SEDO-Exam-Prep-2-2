pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup .NET') {
            steps {
                sh 'wget https://dot.net/v1/dotnet-install.sh'
                sh 'chmod +x dotnet-install.sh'
                sh './dotnet-install.sh --channel 6.0 --install-dir $HOME/dotnet'
                env.PATH = "${env.HOME}/dotnet:${env.PATH}"
            }
        }

        stage('Restore') {
            steps {
                sh '$HOME/dotnet/dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh '$HOME/dotnet/dotnet build --no-restore --configuration Release'
            }
        }

        stage('Test') {
            steps {
                sh '$HOME/dotnet/dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            junit '**/TestResults/*.xml'
        }
    }
}