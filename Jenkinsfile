pipeline {
  environment {
    registry = "pavandhub/docker-v2"
    registryCredential = 'dhub_credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('get scm') {
      steps {
	  git branch: 'main', credentialsId: 'git_credentials_new', url: 'https://github.com/pavanmech/hello_world_24-10.git'
       }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":v$BUILD_NUMBER"
        }
      }
    }
    stage('push image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove old docker image') {
      steps{
        sh "docker rmi $registry:v$BUILD_NUMBER"
      }
    }
  }
}
