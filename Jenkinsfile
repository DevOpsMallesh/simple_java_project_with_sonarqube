pipeline {
    agent any
    tools {
        maven 'Maven3' 
    }
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/DevOpsMallesh/simple_java_project_with_sonarqube.git'
            }
        }
     stage('Sonarqube') {
    environment {
        scannerHome = tool 'sonarqube-test'
    }
    steps {
        withSonarQubeEnv('sonarqube-server-test') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
}
}
}

