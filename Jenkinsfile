pipeline{
    agent any
    stages{
        stage("Prepare environment"){
            steps{
                load "version.groovy"
                buildName "${env.MAJOR_VERSION}.${env.MINOR_VERSION}.${env.BUILD_NUMBER}"
            }
        }
        stage("Build application"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'DockerHub-credentials', passwordVariable: 'DOCKER_REGISTRY_PWD', usernameVariable: 'DOCKER_REGISTRY_USER')]) {
                    sh "az account set --subscription 644bbfce-8865-4261-b6c2-4dd0b1f9f596"
                    sh "az aks get-credentials --resource-group kamereon-poc --name kamereon-dev"
                    sh 'docker login -u=${DOCKER_REGISTRY_USER} -p=${DOCKER_REGISTRY_PWD}'
                    sh "skaffold run"
                }
            }
        }
        stage("Deploy application"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'DockerHub-credentials', passwordVariable: 'DOCKER_REGISTRY_PWD', usernameVariable: 'DOCKER_REGISTRY_USER')]) {
                    sh "az account set --subscription 644bbfce-8865-4261-b6c2-4dd0b1f9f596"
                    sh "az aks get-credentials --resource-group kamereon-poc --name kamereon-dev"
                    sh 'docker login -u=${DOCKER_REGISTRY_USER} -p=${DOCKER_REGISTRY_PWD}'
                    sh "skaffold run"
                }
            }
        }
    }
}