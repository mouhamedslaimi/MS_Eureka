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


         stage('Quality') {

        steps {
              withSonarQubeEnv('SonarQube') {
               sh 'mvn -Psonar -Dsonar.sourceEncoding=UTF-8 org.sonarsource.scanner.maven:sonar-maven-plugin:3.0.2:sonar'
              }
             }
        }

	}
}