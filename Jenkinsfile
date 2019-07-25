def my_function(String serverIp, String scriptArgument) {
    def script_content = libraryResource 'my_scripts/test.sh'
    // create a file with script_bash content
    writeFile file: './test.sh', text: script_content
    echo "Execute remote script test.sh..."
    def sshCommand = "ssh username@${serverIp} \'bash -xs\' < ./test.sh ${scriptArgument}"
    echo "Ssh command is: ${sshCommand}"
    sh(sshCommand)
}

pipeline {
    agent any
    stages {
        stage('MyStage') {
        steps {
            script {
                my_script.my_function("192.168.1.1", "scriptArgumentValue")
                }
            }
        }
        stage('Build') {
            steps {
                sh 'wget -O ~/scripts-0.0.10-master.tar.gz  "https://amidostackspkgukstmp.blob.core.windows.net/packages/scripts-0.0.10-master.tar.gz?se=2019-08-17T10%3A45Z&sp=rl&sv=2018-03-28&ss=b&srt=sco&sig=U/kiUqhl2HZ%2BnVM2xjalg420yjH3bHQuDbwOTYzNcs4%3D"'
                sh 'tar -xvzf ~/scripts-0.0.10-master.tar.gz -C "~/DevOps"'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run hello'
            }
        }
    }
}

