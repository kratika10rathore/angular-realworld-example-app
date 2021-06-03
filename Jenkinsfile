pipeline {
 agent any
  environment {
    dockerHome = tool 'Docker'
}
 stages {
     stage('Git Checkout'){
         steps{
            checkout changelog: false, poll: false, scm: [$class: 'GitSCM',
            branches: [[name: '*/master']], 
            doGenerateSubmoduleConfigurations: false,
            extensions: [], submoduleCfg: [],
            userRemoteConfigs: [[credentialsId: 'github', 
            url: 'https://github.com/kratika10rathore/angular-realworld-example-app.git']]]
         }
 }
      stage("Build"){
         steps{
            sh 'npm install'
            sh 'ng build'
       }
 }
      stage("Docker Image Build"){
         steps{
            sh "${dockerHome}/bin/docker ps"
            sh "${dockerHome}/bin/docker  --version"
            sh "${dockerHome}/bin/docker build -t kratika1/Angular:${BUILD_NUMBER} ."

 }
 }
     stage("Docker Image Push"){
	   steps{
           withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'username')]) {
           sh "${dockerHome}/bin/docker login -u ${username} -p ${password}"
           }
           sh "${dockerHome}/bin/docker push kratika1/Angular.${BUILD_NUMBER}"
		}
}
      
  }
        
 }
