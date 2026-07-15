pipeline {
   agent any

   stages {
       stage('Clone') {
           steps {
               git 'https://github.com/rhumbert1/Fast-API-Docker-Example.git'
           }
       }

        stage('Build') {
            steps {
                sh 'docker build -t fastapi-app .'
            }
        }

        stage('Test') {
            steps {
                sh 'pytest > results.txt'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8000:8000 fastapi-app'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'results.txt', allowEmptyArchive: true
        }
        failure {
            mail to: 'developer@example.com',
                 subject: 'Build failed in Jenkins',
                 body: 'The Jenkins build has failed. Check the logs for more details.'
        }
    }
}