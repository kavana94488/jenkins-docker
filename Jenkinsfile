pipeline {
    agent any

    environment {
        imageName = 'kavana97/jenkins-docker'
        registryCredential = 'docker'
        dockerImage = ''
    }

    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/kavana94488/jenkins-docker.git'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    echo "Building Docker image ${imageName}"
                    dockerImage = docker.build(imageName)
                    echo "Docker image built: ${dockerImage}"
                }
            }
        }
        stage('Run Image') {
            steps {
                script {
                    echo "Running Docker image ${imageName}:latest"
                    sh "docker run ${imageName}:latest"
                }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                    echo "Pushing Docker image to registry"
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push("${env.BUILD_NUMBER}")
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
