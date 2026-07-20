pipeline {
  agent none
  environment{
    IMAGE_NAME = 'devopstrainee13/app'
    IMAGE_TAG = "v${BUILD_NUMBER}"
  }
  stages{
    stage('checkout'){
      agent any
      steps{
        checkout scm
      }
    }
    stage('test'){
      agent {
        docker { 
          image 'python:3.11-slim'
          reuseNode true
        }
      }
      steps{
        sh 'python --version'
        sh 'pip install --no-cache-dir -r requirements.txt'
        sh 'python -m pytest -v'
      }
    }
    stage('Build&Push Image'){
      when{
          branch 'main'
      }
      agent any
      steps{
        withCredentials([usernamePassword(credentialsId: 'DOCKER_CREDITS', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
          sh "echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin"
          sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
          sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
        }
      }
    }
  }
}