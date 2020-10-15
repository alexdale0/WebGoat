node {
   def mvnHome
   stage('Preparation') {
      git 'https://github.com/bigspotteddog/WebGoat.git'
      mvnHome = tool 'M3'
   }
   stage('Build') {
      deleteDir()
      checkout scm
      sh "'${mvnHome}/bin/mvn' clean package"
   }
   stage('Policy Evaluation') {
       nexusPolicyEvaluation advancedProperties: '', failBuildOnNetworkError: false, iqApplication: selectedApplication('test-app'), iqStage: 'develop', jobCredentialsId: ''
   }
   stage('Results') {
      archiveArtifacts 'target/*.jar'
   }
}
