pipeline {
    agent any
    stages {
        stage (SCM) {
            steps {
                git branch: 'main', url: 'https://github.com/vamsibyramala/softwaremakers.git'
            }
        }
        stage (build) {
            steps {
                sh 'mvn clean package'
            }
        }
        stage (deploy) {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:8088')], contextPath: 'vamsi', war: '**/*.war'
            }
        }
        node {
            stage('SCM') {
            checkout scm
          }
          stage('SonarQube Analysis') {
            def mvn = tool 'Default Maven';
            withSonarQubeEnv() {
              sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=commit-hooks -Dsonar.projectName='commit-hooks'"
            }
          }
        }
    }
}
