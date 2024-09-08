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
                    dockerImage = docker.build(imageName)
                }
            }
        }
        stage('Run Image') {
            steps {
                script {
                    sh "docker run ${imageName}:latest"
                }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push("${env.BUILD_NUMBER}")
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
