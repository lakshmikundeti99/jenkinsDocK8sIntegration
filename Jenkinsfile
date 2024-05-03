
pipeline{
    agent any
    tools{
        maven 'LocalMaven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/lakshmikundeti99/jenkinsDocK8sIntegration.git']])
                bat 'mvn clean install'
            }
        }
        stage("Build docker image"){
            steps{
                script{
                    bat "docker build -t ldocker9/jenkins-Integration.jar ."
                }
            }
        }
        stage("Push image to DockerHub"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'pwd', variable: 'dockerpwd')]) {
                        bat "docker login -u ldocker9 -p ${dockerpwd}"
                    }
                bat "docker push ldocker9/jenkins-Integration.jar"
                }
            }
        }
    }
    
}


