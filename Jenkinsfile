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
                cleanWs()
            }
        }

        stage ('Build') {
            steps {
                sh 'dotnet build DemoVersion.csproj --configuration Release'
            }
        }
    }
}
