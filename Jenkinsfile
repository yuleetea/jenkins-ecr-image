pipeline {
  environment {
    registry = '770399057626.dkr.ecr.us-east-1.amazonaws.com/jenkins-cicd'
    registryCredential = 'IAM_SAA'
    dockerImage = 'aws-ecr'
  }
  agent any
  stages {
    stage('Build docker image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push image to ECR') {
        steps{
            script{
                docker.withRegistry("https://" + registry, "ecr:us-east-1:" + registryCredential) {
                    dockerImage.push()
                }
            }
        }
    }
  }
}