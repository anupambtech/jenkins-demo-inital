//Declarative

pipeline{
    agent any
       // agent {docker {image 'maven:3.6.3'}}
        stages{
            stage ('Build') {
                steps {
                  //  sh 'mvn --version'
                    echo "build"
                    echo "PATH - $PATH"
                    echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                    echo "BUILD_ID - $env.BUILD_ID"
                    echo "JOB_NAME - $env.JOB_NAME"
                    echo "BUILD_TAG - $env.BUILD_TAG"
                    echo "BUILD_URL - $env.BUILD_URL"
                }
            }
            stage ('Test') {
                steps {
                    echo "test"
                }
            }
            stage ('Integration test') {
                steps {
                    echo "Integration test"
                }
            }
        }
        post {
        always {
            script {
                echo "Build Completed"
            }
        }
        failure {
            script {
                echo "${stage_name} stage failed."
            }
        }
        success {
            script {
                echo "${stage_name} stage pass. I run when success!."
            }
        }
    }
}