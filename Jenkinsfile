pipeline {
    agent any
        environment {
        azure_client    = credentials('terraform')
        azure_tenant_id = credentials('azure_tenant_id')
        azure_subscription_id = credentials('azure_subscription_id')
        docker_dockerfilePath = './'
        docker_imageName = 'hello'
        docker_imageTag = "0.0.$BUILD_ID-$GIT_BRANCH"
        docker_containerRegistry = "$docker_containerRegistryName.azurecr.io"
        docker_containerRegistryName = 'amidostacksacrukstmp'
        kubernetes_ClusterRG = 'amido-stacks-rg-uks-dev'
        kubernetes_ClusterName = 'amido-stacks-cluster-uks-dev'
    }
    stages {
        stage('Acquire Scripts Package') {
            steps {
                sh 'wget -O ~/scripts-0.0.10-master.tar.gz  "https://amidostackspkgukstmp.blob.core.windows.net/packages/scripts-0.0.10-master.tar.gz?se=2019-08-17T10%3A45Z&sp=rl&sv=2018-03-28&ss=b&srt=sco&sig=U/kiUqhl2HZ%2BnVM2xjalg420yjH3bHQuDbwOTYzNcs4%3D"'
                sh 'mkdir ~/DevOps'
                sh 'tar -xvzf ~/scripts-0.0.10-master.tar.gz -C /home/jenkins/DevOps'
                sh 'chmod +x -R /home/jenkins/DevOps'
            }
        }
        stage('Logins') {
            steps {
                sh '/home/jenkins/DevOps/Azure/set-azure-context.sh $azure_tenant_id $azure_subscription_id $azure_client_USR $azure_client_PSW'
                sh 'az acr login --name $docker_containerRegistryName'
                sh '/home/jenkins/DevOps/Azure/set-aks-context.sh $kubernetes_ClusterRG $kubernetes_ClusterName'
            }
        }
        stage('Docker Build & Push') {
            steps {
                sh 'printenv | sort > printenv.sorted && cat printenv.sorted'
                sh 'cd $docker_dockerfilePath'
                sh 'echo "docker build . -t $docker_imageName:$docker_imageTag -t $docker_containerRegistry/$docker_imageName:$docker_imageTag -t $docker_containerRegistry/$docker_imageName:latest"'
                sh 'docker build . -t $docker_imageName:$docker_imageTag -t $docker_containerRegistry/$docker_imageName:$docker_imageTag -t $docker_containerRegistry/$docker_imageName:latest'
                sh 'docker push $docker_containerRegistry/$docker_imageName'
            }
        }
    }
}
