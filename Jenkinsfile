pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'https://github.com/eslemnurgok/visual1']]])
                sh 'mvn clean install'
            }
        }

        stage('Build docker image'){
            steps{
                script{
                    docker.build("demo12:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    docker.image("demo12:${env.BUILD_NUMBER}").run("-d -p 8080:8081 --name demo-container")
                }
            }
        }
    }
}
