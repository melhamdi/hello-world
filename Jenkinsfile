pipeline {
  agent any
  tools {
    maven 'MAVEN_HOME' 
  }
  stages {
    stage ('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    //deploiement sur un serveur tomcat
    
    stage ('Deploy') {
      steps {
        script {
          deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://192.168.0.23:8082')], contextPath: '/pipeline', onFailure: false, war: 'target/*.war' 
        }
      }
    }
  }
}
