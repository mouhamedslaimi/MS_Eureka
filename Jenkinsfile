pipeline {
  agent any

  tools {
    maven 'maven3'
  
  environment {
		DOCKERHUB_CREDENTIALS=credentials('Docker-hub')
	}

  stages {
    stage('Checkout') {
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
    stage('Build image') {
       dockerImage = docker.build("slaimimed/MS_Eureka")
    }
    stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

    
stage('Push') {

			steps {
				sh 'docker push slaimimed/MS_Eureka:latest'
			}
		}
     /*
    stage('Tests Integration') {
      steps {
        withMaven(globalMavenSettingsConfig: 'b4febe6b-7e35-4582-8550-0b05805e27e1', maven: 'maven3', traceability: false) {
          sh "mvn verify"
        }
      }
    }
  
            stage('Quality') {

              environment {
                SCANNER_HOME = tool 'sonar-scanner'
              }
              steps {
                withSonarQubeEnv('sonarqube') {
                  sh "${SCANNER_HOME}/bin/sonar-scanner"
                }
              }
            }
 

    stage('deploy') {
      steps {
        withMaven(globalMavenSettingsConfig: 'b4febe6b-7e35-4582-8550-0b05805e27e1', maven: 'maven3', traceability: false) {
          sh "mvn deploy -DskipTests"
        }
      }
    }
*/
  }
  	post {
		always {
			sh 'docker logout'
		}
	}
}
