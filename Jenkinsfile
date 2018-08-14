pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'echo Build'
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            bat 'echo Test'
          }
        }
        stage('Ui Test') {
          steps {
            bat 'echo UI Test'
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        bat 'echo deploy'
      }
    }
  }
  environment {
    Foo = 'Bar'
  }
}