pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        git(url: 'https://github.com/SabariSri/CI-CD-Pipeline.git', branch: 'blue_ocean', credentialsId: '34b78ab1-3895-4887-8e03-af7a26a8186a')
        tool(name: 'maven', type: 'maven3.8.1')
      }
    }

    stage('Stagging') {
      parallel {
        stage('Compile') {
          environment {
            maven = 'maven3.8.1'
          }
          steps {
            sh 'mvn compile'
          }
        }

        stage('Test') {
          environment {
            maven = 'maven3.8.1'
          }
          steps {
            sh 'mvn test'
          }
        }

        stage('Package') {
          environment {
            maven = 'maven3.8.1'
          }
          steps {
            sh 'mvn package'
          }
        }

      }
    }

    stage('Results') {
      parallel {
        stage('Results') {
          steps {
            junit '**/*.xml'
          }
        }

        stage('Archive') {
          steps {
            archiveArtifacts '**/*.war'
          }
        }

      }
    }

  }
}