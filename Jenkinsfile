pipeline {
    agent any
        environment {
        azure_client    = credentials('terraform')
        azure_tenant_id = credentials('azure_tenant_id')
        azure_subscription_id = credentials('azure_subscription_id')

    }
    stages {
        stage('Build') {
            steps {
                sh 'wget -O ~/scripts-0.0.10-master.tar.gz  "https://amidostackspkgukstmp.blob.core.windows.net/packages/scripts-0.0.10-master.tar.gz?se=2019-08-17T10%3A45Z&sp=rl&sv=2018-03-28&ss=b&srt=sco&sig=U/kiUqhl2HZ%2BnVM2xjalg420yjH3bHQuDbwOTYzNcs4%3D"'
                sh 'mkdir ~/DevOps'
                sh 'tar -xvzf ~/scripts-0.0.10-master.tar.gz -C /home/jenkins/DevOps'
                sh 'chmod +x -R /home/jenkins/DevOps'
            }
        }
        stage('Login') {
            steps {
                sh '/home/jenkins/DevOps/Azure/set-azure-context.sh $azure_tenant_id $azure_subscription_id $azure_client_USR $azure_client_PSW'
            }
        }
    }
}

