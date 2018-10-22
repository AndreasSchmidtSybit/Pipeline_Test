pipeline {
    agent any
    stages {
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
