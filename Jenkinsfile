pipeline {
  agent {
    node {
      label 'linux'
    }

  }
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/zeemlinux/curriculum-app.git', branch: 'dev')
      }
    }

  }
}