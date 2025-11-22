pipeline {
  agent any
  stages {
    stage('Checkout'){steps{checkout scm}}
    stage('Build Docker'){steps{sh 'docker build -t local-ci-demo .'}}
    stage('Run Container'){steps{sh 'docker run -d -p 3000:3000 --name local-demo local-ci-demo'}}
  }
}