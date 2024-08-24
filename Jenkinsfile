pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "webmvctestex_nohttps:${BUILD_NUMBER}"
        REPO_URL = "https://github.com/RichieCai/WebMVCTestEx_NoHttps.git"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }
        stage('Build') {
            steps {
                script {
                    echo "Building Docker Image: ${DOCKER_IMAGE}"
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}").inside {
                        sh 'dotnet test'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo "Deploying Docker Image: ${DOCKER_IMAGE}"
                    docker.image("${DOCKER_IMAGE}").run('-d -p 8080:80')
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}