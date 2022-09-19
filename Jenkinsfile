pipeline {
  agent {
    node {
      label 'devops'
    }

  }
  stages {
    stage('Git Checkout') {
      parallel {
        stage('Git Checkout') {
          steps {
            git(url: 'https://github.com/zeemlinux/curriculum-app.git', branch: 'dev')
          }
        }

        stage('Logs') {
          steps {
            sh 'ls -last'
          }
        }

        stage('Pruning') {
          steps {
            sh 'docker container prune || y'
          }
        }

      }
    }

    stage('Code-secret Checkout') {
      steps {
        sh '''rm trufflehog || true


docker pull gesellix/trufflehog

docker run -t gesellix/trufflehog --json https://github.com/zeemlinux/curriculum-app.git > trufflehog;

cat trufflehog'''
      }
    }

  }
}