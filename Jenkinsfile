#!/usr/bin/env groovy
pipeline {
    agent any
    environment {
        PROJECT_ID = 'automatic-hawk-276011'
        CLUSTER_NAME = 'my-first-cluster-1'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'automatic-hawk-276011'
        NAMESPACE = 'default'
    }

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
        
        stage("Push images to GCR registry") {
            steps {
                    withDockerRegistry([credentialsId: 'gcr:automatic-hawk-276011', url: 'https://gcr.io']) {
                        sh 'docker tag discovery:v1 gcr.io/automatic-hawk-276011/discovery:$BUILD_NUMBER'
                        sh 'docker push gcr.io/automatic-hawk-276011/discovery:$BUILD_NUMBER'
                        sh "docker rmi --force \$(docker images -q discovery:v1 | uniq)"
                        //sh "docker rmi --force \$(docker images -q gcr.io/automatic-hawk-276011/discovery:$BUILD_NUMBER | uniq)"
                    } 
            }
        }

        stage('Deploy to GKE') {
            steps{
                sh "sed -i 's/discovery:latest/discovery:${env.BUILD_NUMBER}/g' ./HELM_TEST/Springboot-Microservice-Demo/templates/discovery_deployment.yaml"
                step([$class: 'KubernetesEngineBuilder',
                      namespace: "${env.NAMESPACE}",
                      projectId: env.PROJECT_ID, 
                      clusterName: env.CLUSTER_NAME, 
                      location: env.LOCATION, 
                      manifestPattern: './HELM_TEST/Springboot-Microservice-Demo/templates/discovery_deployment.yaml', 
                      credentialsId: env.CREDENTIALS_ID, 
                      verifyDeployments: true])
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
