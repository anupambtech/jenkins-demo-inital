//Declarative

pipeline{
        agent {docker {image 'maven:3.6.3'}}
        stages{
            stage ('Build') {
                steps {
                    sh 'mvn --version'
                    echo "build"
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