
pipeline{
  agent any

  environment{
    imageName='kavana97/jenkins-docker'
    registryCredential='kavana@97'
    dockerImage=''
  }


  stages{
   stage('git clone'){
    steps{
     git branch: 'main', url: 'https://github.com/kavana94488/jenkins-docker.git'

    }
   }
   stage('building Image '){
    steps{
        script{
            dockerImage = docker.build imageName
        }
    }
   }
   stage('running image'){
    steps{
        script{
            sh 'docker run ${imageName}:latest'
        }
    }
   }
   stage('deploy image'){
    steps{
        script{
            docker.withRegistry('',registryCredential)
            dockerImage.push(“$BUILD_NUMBER”)
            dockerImage.push('latest')
        }
    }
   }
  }
}
