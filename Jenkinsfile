pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'sudo apt update'
		        sh 'sudo apt install apt-transport-https ca-certificates curl software-properties-common'
		        sh 'curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -'
		        sh 'sudo  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"'
		        sh 'sudo apt update'
		        sh 'sudo apt-cache policy docker-ce'
		        sh 'sudo apt install docker-ce'
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

