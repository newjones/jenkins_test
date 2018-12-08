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
        sh 'docker run -itd -p 80:80 --rm app||true'
      }
    }
    stage ('Test web port'){
      steps{
        sh '/bin/nc -vz localhost 80'
      }
    }
    stage('Tag and Push registry'){
      steps{
        sh 'docker tag app:test app:stable'
      }
    }
  }
}