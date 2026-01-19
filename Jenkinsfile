pipeline {
  agent any

  tools {
    maven "M3"
    jdk "JDK17"
  }

  stages {
    stage('Git Clone') {
      steps {
        git url: 'https://github.com/akxlfekdb/spring-petclinic.git/', branch: 'main'
      }
    }
    // Maven을 이용해 Build한다
    stage('Maven Build') {
      step {
        sh 'mvn -dmaven.test.failire.ignore=true clean package'
      }
      post {
        success {
          echo 'Maven Build Success'
        }
        failure {
          echo 'maven Build Failed'
        }
      }
    }

    
  }
}
