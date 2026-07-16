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
    stage('Build Image'){
      agent any
      steps{
        sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
      }
    }
  }
}
