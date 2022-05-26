pipeline {
    agent {
        docker {
            image 'dotnet-sdk:1.3.1' 
            args '-v /root/.m2:/root/.m2' 
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
                 sh 'dotnet restore DemoVersion.csproj'
            }
        }

        stage ('Build') {
            steps {
                sh 'dotnet build DemoVersion.csproj --configuration Release'
            }
        }

        stage('Build Docker Image') {
            steps{
                sh ('docker build -t teodorakocan/demo:$NEW_VERSION .')
            }
        }

        stage('Push Docker Image Into Docker Hub') {
            steps{
                withCredentials([string(credentialsId: 'Docker_Password', variable: 'Docker_Password')]) 
                {
                    sh ('docker login -u teodorakocan -p $Docker_Password')
                }
                sh ('docker push teodorakocan/demo:$NEW_VERSION')
            }
        }

        stage('Pull Image from Docker Hub') {
            steps{
                sh ('docker pull teodorakocan/demo:$NEW_VERSION')
            }
        }
    }
}
