pipeline {
  agent any
  stages {
    stage('Build & Compile') {
      parallel {
        stage('Build') {
          steps {
            git(url: 'https://github.com/SabariSri/CI-CD-Pipeline.git', branch: 'blue_ocean', credentialsId: '34b78ab1-3895-4887-8e03-af7a26a8186a')
          }
        }

        stage('Compile') {
          steps {
            withMaven(maven: 'maven3.8.1') {
              sh 'mvn compile'
            }

          }
        }

      }
    }

    stage('Tests') {
      parallel {
        stage('Unit Test') {
          steps {
            withMaven(maven: 'maven3.8.1') {
              sh 'mvn -Dtest=TestGreeter#greetShouldIncludeTheOneBeingGreeted test -pl server'
            }

          }
        }

        stage('Integration Test') {
          steps {
            withMaven(maven: 'maven3.8.1') {
              sh 'mvn test'
            }

          }
        }

      }
    }

    stage('Package') {
      steps {
        withMaven(maven: 'maven3.8.1') {
          sh 'mvn package'
        }

      }
    }

    stage('Results') {
      parallel {
        stage('Report') {
          steps {
            junit '**/*.xml'
          }
        }

        stage('Archive ') {
          steps {
            archiveArtifacts '**/*.war'
          }
        }

      }
    }

  }
}