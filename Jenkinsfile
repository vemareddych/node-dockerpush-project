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
    stage("Build image"){
      steps{
        sh 'docker build -t my-node-app:1 .'
        sh 'docker tag cvreddy/my-node-app:1'
      }
    }
    stage("docker push"){
      steps{
        sh 'docker login -u cvreddy -p @p78H06?.@'
        sh 'docker push cvreddy/my-node-app:1'
        
      }
    }
    
  }
}
