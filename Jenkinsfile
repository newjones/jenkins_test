pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t app .'
      }
    }
    stage('Test') {
      steps {
        echo 'Test'
      }
    }
    stage('Deploy'){
      steps{
        sh 'docker run -itd -p 80:80 --rm app'
      }
    }
  }
}