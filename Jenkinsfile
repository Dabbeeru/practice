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
        sudo docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
		  stage('Deploy Image') {
      steps{
        script {
         sudo docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
		   stage('Remove Unused docker image') {
      steps{
        sh "sudo docker rmi $registry:$BUILD_NUMBER"
      }
 }
  
  }
  }
