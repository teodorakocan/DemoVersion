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
        stage ('Clean workspace')
        {
            steps {
                cleanWs()
            }
        }

        stage ('Restore packages'){
            steps {
                 bat 'dotnet restore DemoVersion.csproj'
            }
        }

        stage ('Build') {
            steps {
                bat 'dotnet build DemoVersion.csproj --configuration Release'
            }
        }
    }
}
