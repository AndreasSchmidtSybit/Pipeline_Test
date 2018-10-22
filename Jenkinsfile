pipeline {
    agent any
    parameters {
       booleanParam(name: 'build', defaultValue: true, description: 'Build project')
       booleanParam(name: 'deploy', defaultValue: false, description: 'Deploy project')
       string(name: 'release_version', defaultValue: '', description: 'Release Version to build')
       gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'    
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
             steps {
                bat 'echo some Test'
              }
        }
        stage('Git push tag') {
            steps {
                  bat "echo Jobname : ${env.JOB_NAME}"
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def buildParams = "-T " + params.release_version
                    bat "echo ${buildParams}"
                }
            }
        }
        stage('Github notify') {
            steps {
                githubNotify description: 'This is an example',  status: 'SUCCESS'
            }
        }
    }
    post {
        failure {
            mail (from: 'jenkins.sybit.de',
                  to: 'ast@sybit.de',
                  subject: "Build failed: ${env.JOB_NAME}",
                  body: "Build failed: ${env.JOB_NAME}")
        }
    }
}
