pipeline {
    agent any

    environment{
        NEW_VERSION = sh(
            script: "printf \$(git rev-parse ${GIT_COMMIT})",
            returnStdout: true
        )
        dotnet = '${PATH}:${HOME}/.dotnet/tools'
        dotnetPath = sh(
            script: "printf \${PATH}:${HOME}",
            returnStdout: true
        )
    }

    stages {

        stage ('Clean workspace')
        {
            steps {
                echo "${PATH}:${HOME}/.dotnet/tools"
                echo "${PATH}:${HOME}"
                echo "dotnet"
                echo "${dotnet}"
                echo "${dotnetPath}"
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
