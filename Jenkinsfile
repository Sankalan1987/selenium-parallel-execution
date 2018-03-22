pipeline {
    agent { 
            docker { 
                    image 'aerokube/selenoid:latest-release' 
                    args '-d --name selenoid -p 4444:4444 -v /var/run/docker.sock:/var/run/docker.sock -v /etc/selenoid:/etc/selenoid:ro'
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
