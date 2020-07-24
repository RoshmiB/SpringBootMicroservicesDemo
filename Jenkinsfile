#!/usr/bin/env groovy
pipeline {
    agent any

    stages {
        stage("Git Checkout") {
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
            bitbucketStatusNotify buildState: "SUCCESSFUL"
        }

        failure {
            bitbucketStatusNotify buildState: "FAILED"
        }
    }    

 }
