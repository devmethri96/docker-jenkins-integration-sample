pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devmethri96/docker-jenkins-integration-sample']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t devmethri/docker-jenkins-integration-sample .'
                }
            }
        }
//         stage('Push image to Hub'){
//             steps{
//                 script{
//                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
//                    sh 'docker login -u javatechie -p ${dockerhubpwd}'

// }
//                    sh 'docker push javatechie/devops-integration'
//                 }
//             }
//         }
//         stage('Deploy to k8s'){
//             steps{
//                 script{
//                     kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
//                 }
//             }
//         }
    }
}