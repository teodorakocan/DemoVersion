pipeline {
    agent any

    environment{
        NEW_VERSION = sh(
                script: "printf \$(git rev-parse ${GIT_COMMIT})",
                returnStdout: true
        )
        dotnet ='C:\\Program Files (x86)\\dotnet\\'
    }

    stages {
        stage ('Git Checkout') {
            steps {
                git branch: 'master', credentialsId: 'GitHubCredentials', url: 'https://github.com/teodorakocan/DemoVersion.git'
            }
        }

        stage ('Clean workspace')
        {
            steps {
                cleanWs()
            }
        }

        stage ('Restore packages'){
            steps {
                 sh 'dotnet restore DemoVersion.csproj'
            }
        }

        stage ('Build') {
            steps {
                sh 'dotnet build DemoVersion.csproj --configuration Release'
            }
        }
    }
}
