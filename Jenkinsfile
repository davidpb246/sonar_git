pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/davidpb246/sonar_git', branch: 'main', credentialsId: 'git_creds'
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
       stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'maven-3', type: 'maven'
        withSonarQubeEnv('sonar-server') {
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
}
