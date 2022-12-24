pipeline {
	agent any
	tools {
		maven 'maven3'
	}
	stages {

		stage("Git Checkout") {
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
        	sh 'docker build -t slaimimed/MS_Eureka:latest .'
                echo 'Build Image Completed'
              }
            }

	}
}