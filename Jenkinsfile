pipeline {
  agent any
  stages{
    stage("SCM Checkout"){
      steps{
        checkout scm
      }
    }
    stage("Test"){
      steps{
        sh 'sudo yum install npm -y'
        sh 'npm test'
      }
    }
    
    stage("build"){
      steps{
        sh 'npm run build'
      }
    }
    
  }
}
