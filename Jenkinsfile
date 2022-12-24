pipeline {   
  agent any
   tools {
    maven 'maven3'
  }
  environment {     
    DOCKERHUB_CREDENTIALS= credentials('Docker-hub')     
  }    
  stages {         
    stage("Git Checkout"){           
     steps {
        checkout scm
      }
    }
    stage('build') {
      steps {
        withMaven(globalMavenSettingsConfig: 'b4febe6b-7e35-4582-8550-0b05805e27e1', maven: 'maven3', traceability: false) {
          sh "mvn clean install -DskipTests"
        }
      }
    }
    stage('Build Docker Image') {         
      steps{                
	sh 'sudo docker build -t slaimimed/MS_Eureka:latest .'           
        echo 'Build Image Completed'                
      }           
    }
    stage('Login to Docker Hub') {         
      steps{                            
	sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
	echo 'Login Completed'                
      }           
    }               
    stage('Push Image to Docker Hub') {         
      steps{                            
	sh 'sudo docker push slaimimed/MS_Eureka:latest' 
  echo 'Push Image Completed'       
      }           
    }      
  } //stages 
  post{
    always {  
      sh 'docker logout'           
    }      
  }  
} //pipeline
