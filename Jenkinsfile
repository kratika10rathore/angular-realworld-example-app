pipeline {
 agent any
  
 stages {
     stage('Git Checkout'){
         steps { 
                echo "getting the code from github" 
                git credentialsId: 'Github', url: 'https://github.com/kratika10rathore/angular-realworld-example-app.git'
                
            }
        }
           
      stage("Build App"){
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
     
       stage("Pulling Docker image and running container using ansible"){
      steps{
        sh 'which ansible'
        sh 'ansible --version'
        ansiblePlaybook credentialsId: 'aws-pem', disableHostKeyChecking: true, installation: 'Ansible', playbook: 'ansible-playbook.yml'
        }
   }
  }
        
 }
