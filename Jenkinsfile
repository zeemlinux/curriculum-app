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
        sh '''docker build -f curriculum-front/Dockerfile -t $JOB_NAME:v1.$BUILD_ID .
'''
      }
    }

    stage('Login To Registry') {
      environment {
        DOCKERHUB_USER = 'zeemlinux'
        DOCKERHUB_PASSWORD = 'G0d1sgud!'
      }
      steps {
        sh '''docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD
'''
      }
    }

    stage('Push Image') {
      steps {
        sh 'docker push /curr-app'
      }
    }

  }
}