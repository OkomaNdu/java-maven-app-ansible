pipeline {
    agent any
    stages {
        stage("Copy files to ansible server") {
            steps {
                script {
                    echo "copying all neccessary files to ansible control node"
                    sshagent(['ansible-server-key']) {
                        sh "scp -o StrictHostKeyChecking=no ansible/* root@68.183.193.73:/root"

                        withCredentials([sshUserPrivateKey(credentialsId: 'ec2-server-key-ansible', keyFileVariable: 'keyfile', usernameVariable: 'user')]) {
                            sh 'scp $keyfile root@68.183.193.73:/root/ssh-key.pem'
                        }
                    }
                }
            }
        }
    }
}
