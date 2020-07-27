#!/usr/bin/env groovy
pipeline {
    agent any

    stages {
        stage("Code Checkout") {
            steps {
                checkout scm
            }
        }

        stage("Code build") {
            steps {
                echo 'Building native binary'
                dir('webstore') {
                    sh 'mvn clean build -DskipTests'
                }    
            }
        }

        stage("Code test") {
            steps {
                dir('webstore') {
                    sh 'mvn test'
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
