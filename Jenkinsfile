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

        stage('nmap scan') {
          steps {
            sh '''rm nmap* || true
docker run --rm -v "$(pwd)":/data uzyexe/nmap -sS -sV -oX nmap 192.168.1.8
cat nmap'''
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

    stage('Front end Unit test') {
      parallel {
        stage('Front end Unit test') {
          steps {
            sh 'cd curriculum-front && npm i && npm run test:unit || True'
          }
        }

        stage('Back end unit test') {
          steps {
            sh 'cd curriculum-back && npm i && npm run test:unit || True'
          }
        }

      }
    }

  }
}