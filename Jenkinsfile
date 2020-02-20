pipeline {
environment {
        registryCredential = 'Dockerhub'
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
	      }
  }
  stage('Create container ') {
   steps {
      sh "sudo docker run -d -p 5001:9091 spring-boot-websocket-chat-demo"
	 
    }
  }
  stage('Pushing the docker image to docker hub ') {
   steps {
      sh "sudo docker tag dilleswari/spring-boot-websocket-chat-demo:0.0.1-SNAPSHOTe practice:newbuild"
	  sh "sudo docker container ls"
	  sh "sudo docker push practice:newbuild"
    }
  }
  }
  }
 
 
