pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'apt update'
		        sh 'apt install apt-transport-https ca-certificates curl software-properties-common'
		        sh 'curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -'
		        sh 'add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"'
		        sh 'apt update'
		        sh 'apt-cache policy docker-ce'
		        sh 'apt install docker-ce'
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

