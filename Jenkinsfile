pipeline {
    environment {
        dockerimagename = "aymenzarour/python-app"
        dockerImage = ""
    }

    agent any

    stages {
        stage('Checkout Source') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM', 
                        branches: [[name: 'main']],  
                        doGenerateSubmoduleConfigurations: false, 
                        userRemoteConfigs: [[
                            credentialsId: 'github-token', 
                            url: 'https://github.com/aymenzarour/python-app-prometheus.git'
                        ]]
                    ])
                }
            }
        }

        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build dockerimagename, "-f app/Dockerfile app"
                }
            }
        }

        stage('Pushing Image') {
            environment {
                registryCredential = 'dockerhublogin'
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                        dockerImage.push("latest")
                    }
                }
            }
        }

        stage('Deploying App to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f k8s-rsc/.'
                }
            }
        }
    }
}
