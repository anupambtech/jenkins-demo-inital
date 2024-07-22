//Declarative

pipeline{
        agent any


        stages{
            stage ('Build') {
                steps {
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
    }
}