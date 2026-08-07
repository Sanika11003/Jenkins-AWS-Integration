pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo "Source code downloaded"
      }
    }
    stage('Build') {
      steps {
        echo "Building Application"
      }
    }
    stage('Test') {
      steps {
        echo "Running Test"
      }
    }
    stage('Deploy to ec2') {
      steps {
        sshagent (['ec2-jenkins-key']) {
          sh '''
          scp -o StrictHostKeyChecking=no \
          index.html \
          ec2-user@13.201.22.118:/tmp/index.html
          ssh -o StrictHostKeyChecking=no \
          ec2-user@13.201.22.118 \
          "sudo cp /tmp/index.html /var/www/html/index.html"
          '''
        }
      }
    }
  }
  post {
    success {
      echo "Application deployed successfully"
    }
    failure {
      echo "Deployment failed"
    }
  }
}
