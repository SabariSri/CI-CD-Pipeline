pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        git(url: 'https://github.com/SabariSri/CI-CD-Pipeline.git', branch: 'blue_ocean', credentialsId: '34b78ab1-3895-4887-8e03-af7a26a8186a')
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

    stage('Deploy') {
      steps {
        deploy(adapters: [tomcat9(credentialsId: 'c9d4b8ab-7ebf-456f-a634-bad11f78afaa', path: '', url: 'http://18.219.32.60:8090/')], war: '**/*.war')
      }
    }

  }
}