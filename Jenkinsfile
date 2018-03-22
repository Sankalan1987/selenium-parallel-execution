pipeline {
    agent any
    stages {
       stage('Create Directory') {
            steps {
               sh 'mkdir -p /etc/selenoid'
            }
        }
        stage('Generate Selenoid Configuration File') {
            agent {
                docker {
                    image 'aerokube/cm:1.0.0'
                    args '--rm -v /var/run/docker.sock:/var/run/docker.sock selenoid --last-versions 2 --tmpfs 128 --pull > /etc/selenoid/browsers.json'
                    reuseNode true
                }
            }
            steps {
              echo 'Config Done'
            }
        }
        stage('Start Selenoid') {
            agent {
                docker {
                    image 'aerokube/selenoid:1.1.1' 
                    args '-d --name selenoid -p 4444:4444 -v /var/run/docker.sock:/var/run/docker.sock -v /etc/selenoid:/etc/selenoid:ro'
                    reuseNode true
                }
            }
            steps {
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
