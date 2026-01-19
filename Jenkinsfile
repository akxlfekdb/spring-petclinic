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
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
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
    //Docker Image 생성
    stage('Docker Image Build') {
      steps {
        echo 'Docker Image Build'
      }
    }

    
    //Docker Image Upload
    stage('Docker Image Upload') {
      steps {
        echo 'Docker Image Upload'
      }
    }

    
    //Target *.jar 전송
    stage('SSH Publish') {
      steps {
        echo 'SSH Publish'
      }
    }


    
  }
}
