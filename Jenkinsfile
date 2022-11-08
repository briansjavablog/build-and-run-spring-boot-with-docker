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
                    sh "skaffold build"
                }
            }
        }
        stage("Deploy application"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'DockerHub-credentials', passwordVariable: 'DOCKER_REGISTRY_PWD', usernameVariable: 'DOCKER_REGISTRY_USER')]) {
                    sh "skaffold build"
                }
            }
        }
    }
}