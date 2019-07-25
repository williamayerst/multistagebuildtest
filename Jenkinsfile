pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'wget -O ~/scripts-0.0.10-master.tar.gz  "https://amidostackspkgukstmp.blob.core.windows.net/packages/scripts-0.0.10-master.tar.gz?se=2019-08-17T10%3A45Z&sp=rl&sv=2018-03-28&ss=b&srt=sco&sig=U/kiUqhl2HZ%2BnVM2xjalg420yjH3bHQuDbwOTYzNcs4%3D"'
                sh 'tar -xvzf ~/scripts-0.0.10-master.tar.gz -C "~/DevOps"'
                sh 'pwd'
                sh 'ls -lp1'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run hello'
            }
        }
    }
}

