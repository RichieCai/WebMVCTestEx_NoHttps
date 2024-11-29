pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "webmvctestex_nohttps:${BUILD_NUMBER}"
        REPO_URL = "https://github.com/RichieCai/WebMVCTestEx_NoHttps.git"
		DONTNET_CLI_HOME="C:\\Program Files\\dotnet"
    }t
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
				    // but "cd"
                    bat "dotnet restore"
					
					//Build the application
					bat "dotnet build --configuration Release"
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    bat "dotnet test --no-restore --configuration Release"
                }
            }
        }
        stage('Pulish') {
            steps {
                script {
                    bat "dotnet publish --no-restore --configuration Release --output .\\publish"
                }
            }
        }
    }
    post {
        success {
            echo 'build,test,and publish successful!'
        }
    }
}