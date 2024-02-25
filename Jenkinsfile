pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devmethri96/docker-jenkins-integration-sample']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t devmethri/docker-jenkins-integration-sample .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   //withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) 
                   
                   bat 'docker login -u devmethri -p 8879506645'
                    
                   bat 'docker push devmethri/docker-jenkins-integration-sample'
                }
                
            }
        }
//         stage('Deploy to k8s'){
//             steps{
//                 script{
//                     kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
//                 }
//             }
//         }
    }
}