#!/usr/bin/env groovy
pipeline {
    agent any

    stages {
        
        stage("Code Checkout") {
            steps {
                deleteDir()
                checkout scm
            }
        }

        stage("Code build & docker image creation") {
            steps {
                echo 'Building native binary'
                dir('./MicroserviceDiscoveryServer') {
                    sh '/usr/local/src/apache-maven/bin/mvn clean install -DskipTests'
                }    
            }
        }

        stage("Code test") {
            steps {
                dir('./MicroserviceDiscoveryServer') {
                    sh '/usr/local/src/apache-maven/bin/mvn test'
                }    
            }
        }
        
        stage("Push images to registry") {
            steps {
                script{
                    docker.withRegistry("https://gcr.io", "automatic-hawk-276011") {
                        sh 'docker tag discovery:v1 gcr.io/automatic-hawk-276011/discovery:vtest'
                        sh 'docker push gcr.io/automatic-hawk-276011/discovery:vtest'
                    }
                }    
            }
        }

        stage("Code deploy") {
            steps {
                println "checkout"
            }
        }

    }
    
    post {
        always {
            println "always"
        }

        success {
            println "success"
        }

        failure {
            println "failed"
        }
    }    

 }
