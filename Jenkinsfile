pipeline {
  agent any
  stages {
    stage('Build develop || master') {
      when {
			  branch 'develop' || branch 'master'
		  }
      steps {
        bat 'echo Build'
      }
    }
    stage('Test') {
      parallel {
        stage('some Tests') {
          steps {
            bat 'echo some Test'
          }
        }
        stage('More Tests') {
          steps {
            bat 'echo More Tests'
          }
        }
      }
    }
    stage('Deploy master') {
      when {
			  branch 'master'
		  }
      steps {
        bat 'echo deploy'
      }
    }
  }
  environment {
    Foo = 'Bar'
  }
}
