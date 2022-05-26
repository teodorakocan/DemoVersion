pipeline {
    agent {
        docker 
        { 
            image 'nugardt/msbuild'
        }
    }

    environment{
        NEW_VERSION = sh(
                script: "printf \$(git rev-parse ${GIT_COMMIT})",
                returnStdout: true
        )
    }

    stages {
        stage('NugetRestore') {
            steps {
                bat 'nuget restore "%WORKSPACE%\\DemoVersion.sln"'
            }
        }  
        stage('Build') {
            steps {
                bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\MSBuild\\15.0\\Bin\\MSBuild.exe" "%WORKSPACE%\\DemoVersion.sln" /t:"Clean" /p:Configuration=Release /p:Platform="x64"'
                bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\MSBuild\\15.0\\Bin\\MSBuild.exe" "%WORKSPACE%\\DemoVersion.sln" /t:"Rebuild" /p:Configuration=Release /p:Platform="x64"'
            }
        }
    }
}
