pipeline {
  agent any
  parameters {
       string(name: 'release_version', defaultValue: '', description: 'Release Version to build')
  }
  environment {
      RELEASE_VERSION = credentials("${params.release_version}")
  } 
  stages {
    stage('Build develop || master') {
      when {
	  expression {
             env.BRANCH_NAME == 'master' || env.BRANCH_NAME == 'develop' && RELEASE_VERSION != '';
    	  }
      }
      steps {
	      bat 'echo build with version:' + RELEASE_VERSION + ', 1.Versuch'
	      bat 'echo build with version:' + $params.release_version + ', 2.Versuch'
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
