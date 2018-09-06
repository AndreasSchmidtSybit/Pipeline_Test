pipeline {
  agent any
  stages {
    stage('Build develop') {
      when {
			  branch 'develop'
		  }
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
