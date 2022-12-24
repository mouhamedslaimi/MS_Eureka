/*
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
		*/
/*
		 stage('Tests Integration') {
              steps {
                withMaven(globalMavenSettingsConfig: 'b4febe6b-7e35-4582-8550-0b05805e27e1', maven: 'maven3', traceability: false) {
                  sh "mvn verify"
                }
              }
            }
*/
/*
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

	}
}
*/
pipeline{
agent any
	tools {
		maven 'maven3'
	}
		environment {
    		DOCKERHUB_CREDENTIALS=credentials('Docker-hub')
    	}

	stages {

	    	stage("Git Checkout") {
        			steps {
        				checkout scm
        			}
        		}
        		stage('build project') {
        			steps {
        				withMaven(globalMavenSettingsConfig: 'b4febe6b-7e35-4582-8550-0b05805e27e1', maven: 'maven3', traceability: false) {
        					sh "mvn clean install -DskipTests"
        				}
        			}
        		}

		stage('Build image') {

			steps {
				sh 'docker build -t slaimimed/MS_Eureka:latest .'
			}
		}


	}



}
