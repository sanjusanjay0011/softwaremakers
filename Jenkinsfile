pipeline {
    stage('SonarQube Analysis') {
            def mvn = tool 'Default Maven';
            withSonarQubeEnv() {
              sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=commit-hooks -Dsonar.projectName='commit-hooks'"
            }
          }
}
