#!/usr/bin/env groovy
pipeline {
    agent any

    stages {
        stage("Code Checkout") {
            steps {
                println "checkout"
            }
        }

        stage("Code build") {
            steps {
                println "checkout"
            }
        }

        stage("Code test") {
            steps {
                println "checkout"
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
