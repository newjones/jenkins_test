pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t app:test .'
      }
    }
    stage('Test') {
      steps {
        echo 'Test'
      }
    }
    stage('Deploy'){
      steps{
        withDockerServer([uri: 'tcp://10.0.0.111:2376']) {
          sh 'docker run -itd -p 80:80 --name app --rm app'
      }
    }
    stage ('Test web port'){
      steps{
        sh '/bin/nc -vz localhost 80'
      }
      post{
        success{
          sh 'docker container stop app'
        }
      }
    }
    stage('Tag and Push registry'){
      steps{
        sh 'docker tag app:test app:stable'
      }
    }
  }
}