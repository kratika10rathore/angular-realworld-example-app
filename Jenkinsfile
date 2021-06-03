pipeline {
 agent any
  
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
      stage("Building image, tagging and pushing it to docker hub"){
         steps{
            sh "sudo docker build -t $myimage ."
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'password', usernameVariable: 'username')]) {
                sh "sudo docker login -u ${username} -p ${password}"
} 
               sh "sudo docker tag $myimage kratika1/dockerclass:$tagname"
               sh "sudo docker push kratika1/dockerclass:$tagname"
            }
        }
     
      
  }
        
 }
