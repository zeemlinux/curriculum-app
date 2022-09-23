pipeline {
  agent {
    node {
      label 'devops'
    }

  }
  stages {
    stage('Git checkout') {
      parallel {
        stage('Git checkout') {
          steps {
            git(url: 'https://github.com/zeemlinux/curriculum-app.git', branch: 'dev')
          }
        }

        stage('Git Secret') {
          steps {
            sh '''rm trufflehog || true
docker pull gesellix/trufflehog
docker run -t gesellix/trufflehog --json https://github.com/zeemlinux/curriculum-app.git > trufflehog
cat trufflehog'''
          }
        }

      }
    }

    stage('List Content') {
      steps {
        sh 'ls -last'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile . -t zeemlinux/curr-app'
      }
    }

  }
}