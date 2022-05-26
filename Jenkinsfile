pipeline {
    agent any

    environment{
        NEW_VERSION = sh(
                script: "printf \$(git rev-parse ${GIT_COMMIT})",
                returnStdout: true
        )
    }

    stages {

        stage ('Clean workspace')
        {
            steps {
                echo "${PATH}:${HOME}"
                cleanWs()
            }
        }

        stage ('Restore packages'){
            steps {
                sh "export PATH=${PATH}:${HOME}/.dotnet/tools"
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
