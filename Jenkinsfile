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
    }    stage('SonarCloud Analysis') {
      environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
      }
      steps {
        sh '''
          wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
          unzip sonar-scanner-cli-5.0.1.3006-linux.zip
          ./sonar-scanner-*/bin/sonar-scanner
        '''
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

