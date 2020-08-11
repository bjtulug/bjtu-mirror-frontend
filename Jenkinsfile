pipeline {
  agent any
  environment {
    HOME = '.'
  }
  stages {
    stage('Start') {
      agent { 
        docker {
          image 'node:lts-alpine'
          args '-v /home/bob/public:/tmp/public'
        } 
      }
      stages{
        stage('Enviroument') {
          steps {
            sh 'ln -s /tmp/public public'
            sh 'npm install'
          }
        }
        stage('Build') {
          steps {
            sh 'npx hexo generate && npx hexo deploy'
          }
        }
      }
    }
  }
}
