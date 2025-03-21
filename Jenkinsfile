//Declarative

pipeline{
    agent any
       // agent {docker {image 'maven:3.6.3'}}
       environment{
        dockerHome= tool 'myDocker'
        mavenHome= tool 'myMaven'
        PATH="$dockerHome/bin:$mavenHome/bin:$PATH"
       }

    parameters {
        choice(name: 'environment', choices: "sandbox\nstaging\nproduction", description: 'Select Environment')
        choice(name: 'suiteXmlFile', choices: "BillingSuite.xml\nCoreAPISuite.xml\nvisualizerTesting.xml", description: 'Select Test suite')
        string(name: 'tags', defaultValue: '@Retrieve', description: 'Tag[s] to run specific tests')
    }

        stages{
            stage ('Checkout') {
                steps {
                    sh 'mvn --version'
                    sh 'docker --version'
                    echo "build"
                    echo "PATH - $PATH"
                    echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                    echo "BUILD_ID - $env.BUILD_ID"
                    echo "JOB_NAME - $env.JOB_NAME"
                    echo "BUILD_TAG - $env.BUILD_TAG"
                    echo "BUILD_URL - $env.BUILD_URL"
                }
            }
            stage("Build"){
                steps{
                    sh "mvn clean compile"
                }
            }
            stage ('Test') {
                steps {
                    sh 'mvn test'
                    echo "test"
                }
            }
            stage ('Integration test') {
                steps {
                    echo "Integration test"
                }
            }
            stage ('Package') {
                steps {
                    sh 'mvn package -DskipTests'
                }
            }
            stage ('Build docker Image') {
                steps {
                    //sh 'docker build -t anupam2485/jenkins-demo-initial:$env.BUILD_TAG'
                    script{
                        dockerImage=docker.build("anupam2485/jenkins-demo-initial:${env.BUILD_TAG}")
                    }
                }
            }
            stage ('Push docker image') {
                steps {
                    script{
                        docker.withRegistry('','927f90e7-6cd4-4191-9209-9c4b9ee96a2d'){
                        dockerImage.push();
                        dockerImage.push('latest')
                        }
                    }
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