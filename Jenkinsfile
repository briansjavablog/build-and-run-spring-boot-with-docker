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
                    sh 'docker login -u=${DOCKER_REGISTRY_USER} -p=${DOCKER_REGISTRY_PWD}'
                    sh "skaffold run"
                }
            }
        }
        stage("Deploy application"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'DockerHub-credentials', passwordVariable: 'DOCKER_REGISTRY_PWD', usernameVariable: 'DOCKER_REGISTRY_USER')]) {
                    sh 'docker login -u=${DOCKER_REGISTRY_USER} -p=${DOCKER_REGISTRY_PWD}'
                    sh "skaffold run"
                }
            }
        }
    }
}