pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
	agent none
      stages{
           stage('Checkout'){
              agent any
              steps{
		 echo 'cloning in master..'
                 git 'https://github.com/preshcode007/DevOpsCodeDemo.git'
              }
          }
          stage('Compile'){
              agent {label 'slave1'}   
              steps{
                  echo 'compiling in slave1..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
              agent {label 'slave2'}
              steps{
		    
		  echo 'codeReview in slave2'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
              agent (label 'slave1')
              steps{
	         echo 'Testing in slave1'
                  sh 'mvn test'
              }
               post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }	
          }
          stage('Package'){
              agent any
              steps{
                  sh 'mvn package'
              }
          }
      }
}
