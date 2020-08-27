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
   
 
sh 'sudo docker build -t dilleswari/tomcat:2.0 .'

 
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

 
sh 'sudo docker push dilleswari/tomcat:2.0'

 
}

 
}
        stage('Deployment in cluster'){
steps('cluster'){
withKubeConfig(credentialsId: 'kubernetes') {
sh 'kubectl  apply -f deployment.yml '


    }
}
