pipeline {
  agent docker
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
        echo 'DEPLOY'
      }
    }
  }
}