pipeline {
    agent any
    stages {
       
        stage('Start Selenoid') {
            agent {
                docker {
                    image 'aerokube/cm:latest-release' 
                    args '--rm -v /var/run/docker.sock:/var/run/docker.sock -v ${HOME}:/root -e OVERRIDE_HOME=${HOME}'
                    reuseNode true
                }
            }
            steps {
                sh 'selenoid start --vnc --tmpfs 128'
              echo 'Selenoid Started'
            }
        }
        stage('Build Project') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v $HOME/.m2:/root/.m2'
                    reuseNode true
                }
            }
            steps {
               sh 'mvn clean install'
            }
        }
    }
}
