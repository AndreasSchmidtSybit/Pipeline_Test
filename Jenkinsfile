pipeline {
    agent any
    parameters {
       string(name: 'release_version', defaultValue: '', description: 'Release Version to build')
    }
    stages {
        stage('build') {
            when {
                expression {
                     env.BRANCH_NAME == 'develop' && params.release_version == '';
                }
            }
            steps {
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
                          bat "echo Jobname : ${env.JOB_NAME}"
                    }
                }
            }
        }
        stage('build') {
            when {
                expression {
                     env.BRANCH_NAME == 'develop' && params.release_version == '';
                }
            }
            steps {
                stage('release') {
                    steps {
                        bat 'echo release'
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