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
                script {
                withSonarQubeEnv('sonarqube-server-test'){
                sh "mvn sonar:sonar"
                    }
            timeout(time: 1, unit: 'HOURS') {
            def qqstate=waitForQualityGate()
            if (qqstate.status !='ok'){

	            error "pipeline failed ${qqstate.status}"
	            }
	        }
        sh mvn clean install
        }
        }
    }
}
}

