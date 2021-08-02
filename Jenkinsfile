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
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube-server-test') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'Maven3') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}

