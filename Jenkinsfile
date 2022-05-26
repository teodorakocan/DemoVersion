pipeline {
    agent {
        docker {
            image 'bitnami/dotnet-sdk:latest' 
            args '-v /path/to/dotnet-persistence:/bitnami' 
        }
    }

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

        stage ('Restore packages'){
            steps {
                 sh 'dotnet --version'
            }
        }

        
    }
}
