pipeline {
  agent {
    node {
      label 'main'
    }
  }
  environment {
    HOME = '.'
  }
  stages {
    stage('Start') {
      agent { 
        docker {
          label 'main'
          image 'node:lts-alpine'
          args '-v /home/bob/public:/tmp/public -v npm_cache:/home/node/.npm'
        } 
      }
      stages{
        stage('Enviroument') {
          steps {
            sh 'ln -s /tmp/public public'
            sh 'sed -i \'/"resolved":/d\' package-lock.json || exit 0'
            sh 'npm config set registry https://npm-registry.mirror.bjtulug.org'
            sh 'npm ci'
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
