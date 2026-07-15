pipeline {
  agent none

  stages{
    stage('checkout'){
      agent any
      steps{
        checkout scm
      }
    }
    stage('test'){
      agent {
        docker { image 'python:3.11-slim' }
      }
      steps{
        sh 'python --version'
        sh 'pip install --no-cache-dir -r requirements.txt'
        sh 'python -m pytest -v'
      }
    }
  }
}
