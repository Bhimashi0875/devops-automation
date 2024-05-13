pipeline {
    agent any
    tools {
        maven 'maven-3'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Bhimashi0875/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    bat 'docker build -t bhimashi/devops-integration .'
                }
            }
        }
        stage('Push image to Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerpwd-hub', variable: 'docker-hub')]) {
                        bat 'docker login -u bhimashi -p ${docker-hub}'
                }
                bat 'docker push bhimashi/devops-integration'
                }
            }
        }
    }
}