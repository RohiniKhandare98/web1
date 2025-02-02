pipeline {
    agent any
    stages {
        
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/RohiniKhandare98/web1.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh "/usr/local/bin/docker image build -t rohini1/web11 ."
            }
        }
        
        stage("Push docker image") {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_HUB_TOKEN', variable: 'DOCKER_HUB_TOKEN')]) {
                    sh "echo $DOCKER_HUB_TOKEN | /usr/local/bin/docker login -u rohini1 --password-stdin"
                    sh "/usr/local/bin/docker image push rohini1/web11"
                }
            }
        }
        
        stage("Deploy docker service") {
            steps {
  //             sh "/usr/local/bin/docker service rm backend"
                sh "/usr/local/bin/docker service create --name web1 -p 4000:4000 --replicas 2 rohini1/web11"
            }
        }
        
    }
}
