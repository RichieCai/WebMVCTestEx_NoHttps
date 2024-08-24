pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/RichieCai/WebMVCTestEx_NoHttps.git'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build'
            }
        }
        stage('Test') {
            steps {
                sh 'dotnet test'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
						// 使用當前項目目錄下的 Dockerfile 構建 Docker 映像
						def dockerImage = docker.build("webmvctestex_nohttps:latest")
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // 刪除已有的容器，避免名稱衝突
                    sh 'docker rm -f webmvctestex_nohttps-container || true'
                    
                    // 運行新構建的 Docker 映像
                    sh 'docker run -d -p 5300:80 --name yourproject-container webmvctestex_nohttps:latest'
                    }
                }
            }
        }
    }
}
