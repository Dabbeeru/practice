#!/usr/bin/env bash
pipeline {
    agent {
        label 'master'
    }

    // Build stages:
    stages {

        stage('Install necessary modules') {
            steps {
                sh "mvn clean install"
            }
        }

        stage('Run Sonar Scanner') {
            steps {
                sh "mvn verify sonar:sonar"
            }
        }

      //  stage('Deploy the code to tomcat') {
        //    steps {
          //      sh "mvn tomcat7:redeploy"
          //  }
       // }
        stage ('building docker image'){

 
steps

 
{

 
echo "building the docker image "
   
 
sh '$ docker build -t spring-boot-websocket-chat-demo .'

 
}

 
}

 
  
stage('Push the docker image to hub'){

 
steps

 
{

 
echo "login into docker hub "

 
withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'passwd', usernameVariable: 'username')])

 
{

 
sh 'sudo docker login -u ${username} -p ${passwd}'

 
}

 
sh 'sudo docker push dilleswari/spring-boot-websocket-chat-demo'

 
}

 
}
        stage('Run kubectl') {
      steps ('kubectl') 
            {
        sh "kubectl get pods"
      }
    }

    }
}
