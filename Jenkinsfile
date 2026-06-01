pipeline {
    agent any

    stages {
        stage('Cleaning workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Cloning repo') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/maxskomorohov/petclinic.git'
                sh "ls -la"
            }
        }

        stage('Docker Build') {
            steps {
                sh "docker build -t petclinic:latest -t maks1020/petclinic-new:latest ."
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_hub_secret', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "docker login -u ${USER} -p ${PASS}"
                    sh "docker push maks1020/petclinic-new:latest"
                }
            }
        }

    }
}
