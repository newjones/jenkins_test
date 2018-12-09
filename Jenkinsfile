pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        withDockerServer([credentialsId: 'jenkins-docker-test', uri: 'tcp://10.0.0.111:2376']) {
          sh 'docker build -t app:test .'
        }
      }
    }
    stage('Deploy'){
      steps{
        withDockerServer([credentialsId: 'jenkins-docker-test', uri: 'tcp://10.0.0.111:2376']) {
          sh 'docker run -itd -p 80:80 --name app --rm app'
        }
      }
    }
    stage ('Test web port'){
      steps{
        sh '/bin/nc -vz localhost 80'
      }
      post{
        success{
          withDockerServer([credentialsId: 'jenkins-docker-test', uri: 'tcp://10.0.0.111:2376']) {
            sh 'docker container stop app'
          }
        }
      }
    }
    stage('Tag and Push registry'){
      steps{
        withDockerServer([credentialsId: 'jenkins-docker-test', uri: 'tcp://10.0.0.111:2376']) {
          sh 'docker tag app:test app:stable'
        }
      }
    }
  }
}