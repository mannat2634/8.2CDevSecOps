pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/mannat2634/8.2CDevSecOps.git'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Run Tests') {
      steps {
        sh 'npm test || true'
      }
    }
    stage('Security Scan') {
      steps {
        sh 'npm audit || true'
      }
    }
  }

  post {
    always {
      emailext (
        subject: "Build Status: ${currentBuild.currentResult}",
        body: "The build ${currentBuild.fullDisplayName} has finished with status: ${currentBuild.currentResult}",
        to: "sharmamannat2634@gmail.com",
        attachLog: true
      )
    }
  }
}

