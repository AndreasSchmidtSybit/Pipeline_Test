pipeline {
  agent any
  parameters {
       string(name: 'release_version', defaultValue: '', description: 'Release Version to build')
  }
  stages {
    stage('Build develop || master') {
      when {
	  expression {
             env.BRANCH_NAME == 'master' || env.BRANCH_NAME == 'develop' && RELEASE_VERSION != '';
    	  }
      }
      steps {	      
	      bat 'echo build with version:' + params.release_version
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
  post {
        failure {
            mail (to: ast@sybit.de,
                  subject: 'Build $JOB_NAME failed')
        }
  }
}
