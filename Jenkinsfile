pipeline {
    agent { 
            docker { 
                    image 'elgalu/selenium' 
                    args '--privileged -d --name=grid -p 4444:24444 -p 5900:25900 -e TZ="America/Sao_Paulo" -e VNC_PASSWORD=passwd -v /dev/shm:/dev/shm'
                } 
            }
    stages {
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