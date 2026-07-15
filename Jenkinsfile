pipeline {
  agent any

  stages{
    stage('test'){
      agent {
        docker { image 'python:3.11-slim' }
      }
      steps{
        sh 'python --version'
        sh 'pip install -r --no-cache-dir requirements.txt'
        sh 'pytest -v'
      }
    }
  }
}
