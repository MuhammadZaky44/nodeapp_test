pipeline {
    environment {
        dockerimagename = "zakyfatih/nodeapp"
        dockerImage = ""
    }

    agent any

    stages {
        stage('Checkout Source') {
            steps {
                git 'https://github.com/MuhammadZaky44/nodeapp_test.git'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build dockerimagename
                }
            }
        }

        stage('Push Docker Image'){
             steps {
                 withCredentials([usernamePassword(credentialsId: 'dockerhub-zaky', passwordVariable: 'pass', usernameVariable: 'user')]) {
                     sh "docker login -u $user --password $pass"
                     sh "docker push zakyfatih/nodeapp:latest"
                     sh "docker push zakyfatih/nodeapp:latest"
                 }
             }
         }

         stage('Deploy to Kubernetes'){
             steps {
                script {
                    kubernetesDeploy(configs: deploymentservice.yml, kubeconfigId: "kubernetes")
                }
             }
         }

    }
}