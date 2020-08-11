pipeline {
  agent any
  environment {
    HOME = '.'
  }
  stages {
    stage('Start') {
      agent { docker 'node:lts-alpine' }
      stages{
        stage('Enviroument') {
          steps {
            sh 'npm install'
          }
        }
        stage('Build') {
          steps {
            sh 'npx hexo generate && npx hexo deploy'
          }
        }
        stage('Check') {
          steps {
            echo 'Hello world'
            sh 'sleep 10 && ls'
          }
        }
      }
    }
  }
}
