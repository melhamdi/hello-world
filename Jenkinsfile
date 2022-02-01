pipeline {
  agent any
  tools {
    maven 'MAVEN_HOME' 
  }
  stages {
    stage ('Compilation') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage ('Deploiement') {
      steps {
        script {
          deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://192.168.0.21:8082')], contextPath: '/pipeline', onFailure: false, war: 'target/*.war' 
        }
      }
    }
  }
}
