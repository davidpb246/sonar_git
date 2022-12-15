node{
// demo
   stage('SCM Checkout'){
     git 'https://github.com/davidpb246/sonar_git'
     git url: 'https://github.com/davidpb246/sonar_git', branch: '*/main',
        credentialsId: 'git_creds'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'
      sh "${mvnHome}/bin/mvn package"
   }

   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'maven-3', type: 'maven'
        withSonarQubeEnv('sonar-server') {
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
}
