pipeline {
  agent any

  tools {
    maven "M3"
    jdk "JDK17"
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerCredential')
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
        dir("${env.WORKSPACE}") {
          sh """
          docker build -t spring-petclinic:$BUILD_NUMBER .
          docker tag spring-petclinic:$BUILD_NUMBER akxlfekdb/spring-petclinic:latest
          """ 
        }
      }
    }
 
    
    //Docker Image Upload
    stage('Docker Image Upload') {
      steps {
        echo 'Docker Image Upload'
        sh """
          echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
          docker push akxlfekdb/spring-petclinic:latest
          """
      }
    }

    
    


    
  }
}
