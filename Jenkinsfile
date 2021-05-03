pipeline {
    agent any

    tools {
        maven 'maven3.8.1'
    }

    stages {
        stage('Build') {
            steps {
                git branch: 'main', credentialsId: 'b71466d5-515a-4721-9253-f0c6d3a97770', url: 'https://github.com/SabariSri/CI-CD-Pipeline'
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
        stage('Results') {
            steps {
               junit '**/*.xml'
               archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
         stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '78721f39-0953-49ef-844e-71543b04843c', path: '', url: 'http://3.19.14.45:8090/')], contextPath: null, war: '**/*.war'            }
        }
    }    
}
