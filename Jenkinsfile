pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME'
    }
    environment {
        DATE = new Date().format('yy.M')
        registry = "melhamdi/rep01"
        TAG = "${DATE}.${BUILD_NUMBER}"
    }
    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }


        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub_id', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                    sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                    sh "docker push $registry:$TAG"
                }
            }
        }
    }
}
