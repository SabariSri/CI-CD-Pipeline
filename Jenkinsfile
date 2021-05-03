pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/neelasandeep/CICD', branch: 'master')
      }
    }

    stage('test') {
      parallel {
        stage('test') {
          steps {
            withMaven(maven: 'Maven') {
              sh 'mvn test'
            }

          }
        }

        stage('package') {
          steps {
            withMaven(maven: 'Maven') {
              sh 'mvn package'
            }

          }
        }

      }
    }

    stage('results') {
      steps {
        archiveArtifacts '**/*.war'
        junit '**/*.xml'
      }
    }

  }
}