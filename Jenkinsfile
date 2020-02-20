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
 stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
		  stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
		   stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
 }
  stage('Pushing the docker image to docker hub ') {
   steps {
      sh "sudo docker tag dilleswari/spring-boot-websocket-chat-demo:0.0.1-SNAPSHOT practice:newbuild"
	  sh "sudo docker container ls"
	   sh'sudo docker login -u dilleswari -p l@xmi321'
	   sh "sudo docker push practice:newbuild"
    }
  }
  }
  }
