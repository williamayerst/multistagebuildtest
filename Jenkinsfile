pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
		        sh 'docker build . -t hello'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run hello'
            }
        }
    }
}

