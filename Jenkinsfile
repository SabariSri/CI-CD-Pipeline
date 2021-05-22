pipeline {
  agent any
  stages {
    stage('Compile') {
      agent {
        node {
          label 'master'
        }

      }
      environment {
        mvn = '1.8'
      }
      steps {
        sh 'mvn compile'
      }
    }

  }
}