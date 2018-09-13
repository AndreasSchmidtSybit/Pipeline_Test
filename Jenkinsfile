pipeline {
    agent any
    parameters {
       string(name: 'release_version', defaultValue: '', description: 'Release Version to build')
    }
    stages {
        stage('Build develop || master') {
            when {
                expression {
                     env.BRANCH_NAME == 'master' || env.BRANCH_NAME == 'develop' && params.release_version != '';
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
        stage('Git push tag') {
            steps {
                //sshagent(['jenkins']) {
                      bat 'Jobname 1 :' + $JOB_NAME
                      bat 'Jobname 2 :' + JOB_NAME
                      bat 'Jobname 3 :' + ${JOB_NAME}
                      bat 'Jobname 4 :' + ${env.JOB_NAME}
                      bat 'Jobname 5 :' + env.JOB_NAME
                      bat 'Jobname 6 :' + $env.JOB_NAME
                //}
            }
        }
    }
    post {
        failure {
            mail (from: 'jenkins.sybit.de',
                  to: 'ast@sybit.de',
                  subject: 'Build' +  JOB_NAME + ' failed',
                  body: '')
        }
    }
}