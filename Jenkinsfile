pipeline {
    agent any
    environment {
        scannerHome = tool 'sonarqube-test'
    }
    tools {
    maven 'Maven3'
  }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'master', credentialsId: 'f982a97f-4c9c-4f01-abf2-f5befc5d305d', url: 'https://github.com/DevOpsMallesh/simple_java_project_with_sonarqube.git'
            }
        }
		stage("SonarQube analysis") {
           
            steps {
				script{
              withSonarQubeEnv('sonarqube-test') {
                //sh 'mvn sonar:sonar'
		      //sh "${scannerHome}/bin/sonar-scanner"
		      sh 'mvn clean package sonar:sonar'
				}
				}
				}
				}
		stage("Quality Gate and build") {
			steps{
              timeout(time: 1, unit: 'HOURS') {
              waitForQualityGate abortPipeline: true
              }
            }
          }
		  
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
    }
}


