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

    stage ('Git Checkout')
    {
      steps {
         git branch: 'master', credentialsId: 'GitHubCredentials', url: 'https://github.com/teodorakocan/DemoVersion.git'
      }
    }

    stage ('Restore packages'){
      steps {
        bat "dotnet restore DemoVersion\\DemoVersion.csproj"
      }
    },
    stage ('Build') {
      steps {
        "bat" "dotnet build DemoVersion\\DemoVersion.csproj --configuration Release"
      }
    }
  }
}
