pipeline {
  agent any
  stages {
    stage ("Checkout code") {
      steps {
        checkout scm
      }
    }
    stages {
    stage("Deploy site") {
      steps {
        sh 'cp index.json /var/www/html'
      }
    }
    stage ("Run HawkScan Test") {
      environment {
        STACKHAWK_API_KEY = credentials('stackhawk-api-key')
      }
      steps {
        sh '''
          docker run -v ${WORKSPACE}:/hawk:rw -t \
            -e API_KEY=${HAWK_API_KEY} \
            -e NO_COLOR=true \
            stackhawk/hawkscan
        '''
      }
    }
  }
}
