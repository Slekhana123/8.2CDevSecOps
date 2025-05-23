pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Slekhana123/8.2CDevSecOps.git'
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

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan') {
      steps {
        sh 'npm audit || true'
      }
    }
  }

  post {
    always {
      emailext(
        to: 'e.lekhana123@gmail.com',
        subject: "Jenkins Build - ${currentBuild.currentResult}",
        body: "Build Result: ${currentBuild.currentResult}\nProject: ${env.JOB_NAME}\nBuild URL: ${env.BUILD_URL}",
        attachLog: true
      )
    }
  }
}
