pipeline {
  agent any
  stages {
    stage('Build develop || master') {
      when {
	  expression {
             env.BRANCH_NAME == 'master' || env.BRANCH_NAME == 'develop';
    	  }
      }
      steps {
	      withEnv(["GIT_BRANCH=$BRANCH_NAME"]) {
		      bat 'echo ${GIT_BRANCH}'
		      bat 'echo $GIT_BRANCH'		      
	      }
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
