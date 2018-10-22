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
                githubNotify account: 'AndreasSchmidtSybit', context: 'Test', credentialsId: '8bffabf3-ab73-4312-9356-bbe7e1c278c3',
				status: 'SUCCESS', targetUrl: 'https://github.com/AndreasSchmidtSybit/',
				description: 'This is an example', repo: 'Pipeline_Test', sha: 'db70f743fd4927d36ccaa998b11d639c88aed4dd'
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
