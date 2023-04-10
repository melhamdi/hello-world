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
                    // docker.build("vigneshsweekaran/hello-world:${TAG}")
                    //dockerImage = docker build -t myimages:${TAG} -f Dockerfile ."
                    dockerImage = docker.build("${registry}:${TAG}")
                }
            }
        }
        //	  stage('Pushing Docker Image to Dockerhub') {
        //            steps {
        //              script {
        //                docker.withRegistry('https://registry.hub.docker.com', 'docker_credential') {
        //                  docker.image("melhamdi/myimages:${TAG}").push()
        //                docker.image("melhamdi/myimages:${TAG}").push("latest")
        //         }
        //   }
        //}
        //}
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
