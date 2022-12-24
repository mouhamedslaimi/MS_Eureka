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

		 stage('Tests Integration') {
              steps {
                withMaven(globalMavenSettingsConfig: 'b4febe6b-7e35-4582-8550-0b05805e27e1', maven: 'maven3', traceability: false) {
                  sh "mvn verify"
                }
              }
            }


            stage('SonarQube analysis') {
              tools {
                sonarQube 'SonarQube Scanner 2.8'
              }
              steps {
                withSonarQubeEnv('SonarQube Scanner') {
                  sh 'sonar-scanner'
                }
              }
            }

	}
}