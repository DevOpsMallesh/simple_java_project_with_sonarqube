pipeline {
    agent any
    tools {
    maven 'Maven3'
  }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'f982a97f-4c9c-4f01-abf2-f5befc5d305d', url: 'https://github.com/DevOpsMallesh/HCL_SampleApplication.git'
            }
        }
		stage("SonarQube analysis") {
           
            steps {
				scripts{
              withSonarQubeEnv('SonarQubeJenkins') {
                sh 'mvn sonar:sonar'
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
		stage("deploy in tomcat with ansible"){
		steps{
			ansiblePlaybook become: true, credentialsId: 'Jenkins-Slave', inventory: '$WORKSPACE', playbook: 'ansible_tomcat.yaml'
		}
		}
    }
}


