pipeline {
  agent {
    node {
      label 'devops'
    }

  }
  stages {
    stage('Git checkout') {
      steps {
        git(url: 'https://github.com/zeemlinux/curriculum-app.git', branch: 'dev')
      }
    }

  }
}