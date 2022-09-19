pipeline {
  agent {
    node {
      label 'devops'
    }

  }
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/zeemlinux/curriculum-app.git', branch: 'dev')
      }
    }

    stage('Code Checkout') {
      steps {
        sh '''rm trufflehog || true
docker pull gesellix/trufflehog
docker run -t gesellix/trufflehog --json https://github.com/zeemlinux/curriculum-app.git > trufflehog
cat trufflehog'''
      }
    }

  }
}