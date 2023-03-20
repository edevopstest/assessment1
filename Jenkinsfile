pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git branch: 'main', url: 'https://github.com/edevopstest/assessment1.git'
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build . -t kannanta/assessment1"
            }
        }
        stage('DockerHub Push'){
            steps{
                
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerPwd')]) {
                      sh "docker login -u kannanta -p ${dockerPwd}"
                }
                
                sh "docker push kannanta/assessment1 "
            }
        }        
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-playbook.yml'
            }
        }
    }
}

