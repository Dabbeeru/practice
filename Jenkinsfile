pipeline {
environment {
    registry = "dilleswari/practice"
    registryCredential = 'dockerhub'
  }
          agent any
          stages {
              stage('Checkout external proj') {
                steps {
                    git branch: 'master',
                        
                    url: 'https://github.com/Dabbeeru/practice.git'
        
                    sh "ls -lat"
                }
        		}
				stage('Package') {
   steps {
      sh 'mvn clean package'
	 
    }
  }
 stage('Create Docker Image') {
    steps {
      sh "sudo docker build -t spring-boot-websocket-chat-demo ."
	  sh "sudo docker image ls"
	  sh "sudo usermod -a -G docker $USER"
	  sh " sudo docker login -u dilleswari -p l@xmi321 https://index.docker.io/v1/"
	      }
  }
		  stage('Pushing the docker image to docker hub ') {
   steps {
      sh "sudo docker tag dilleswari/spring-boot-websocket-chat-demo:0.0.1-SNAPSHOT practice:newbuild"
	  sh "sudo docker container ls"
	  sh "sudo docker push dilleswari/spring-boot-websocket-chat-demo:0.0.1-SNAPSHOT"
    }
  }
		   stage('Remove Unused docker image') {
      steps{
        sh "sudo docker rmi $registry:$BUILD_NUMBER"
      }
 }
  
  }
  }
