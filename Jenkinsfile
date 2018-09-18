pipeline {
    agent any
    parameters {
       booleanParam(name: 'build', defaultValue: true, description: 'Build project')
       booleanParam(name: 'deploy', defaultValue: false, description: 'Deploy project')
       string(name: 'release_version', defaultValue: '', description: 'Release Version to build')
    }
    stages {
        stage ('Build') {
            when {
                expression {
                    params.build == true;
                }
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
                stage('Git push tag') {
                    steps {
                          bat "echo Jobname : ${env.JOB_NAME}"
                    }
                }
            }
        }

        stage ('Build') {
            when {
                expression {
                    params.deploy == true && params.release_version != '';
                }
            }
            stages {
                stage('Deploy') {
                    when {
                        branch 'master'
                    }
                    steps {
                        bat 'echo deploy'
                    }
                }
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