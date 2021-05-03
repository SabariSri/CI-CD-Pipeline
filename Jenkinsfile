pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        git(url: 'https://github.com/SabariSri/CI-CD-Pipeline', branch: 'main', credentialsId: 'b71466d5-515a-4721-9253-f0c6d3a97770')
      }
    }

    stage('Test') {
      parallel {
        stage('Compile') {
          steps {
            sh 'mvn compile'
          }
        }

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
  environment {
    maven = 'maven3.8.1'
  }
}