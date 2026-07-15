pipeline {
   agent any

   stages {
       stage('Clone') {
           steps {
               git branch: "main", url: "https://github.com/rhumbert1/Fast-API-Docker-Example.git"
           }
       }

        stage('Build') {
            steps {
                bat 'docker build -t fastapi-app .'
            }
        }

        stage('Test') {
            steps {
                bat 'pytest > results.txt'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker run -d -p 8000:8000 fastapi-app'
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