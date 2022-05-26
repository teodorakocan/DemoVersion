pipeline {
    agent any

    environment{
        NEW_VERSION = sh(
            script: "printf \$(git rev-parse ${GIT_COMMIT})",
            returnStdout: true
        )
        dotnet = '${PATH}:${HOME}/.dotnet/tools'
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
