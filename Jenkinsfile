pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn build'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'mvn test'
          }
        }

        stage('Package') {
          steps {
            sh 'mvn package'
          }
        }

      }
    }

  }
}