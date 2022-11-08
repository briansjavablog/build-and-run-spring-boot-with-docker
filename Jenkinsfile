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
                sh "skaffold build"
            }
        }
        stage("Deploy application"){
            steps{
                sh "skaffold run"
            }
        }
    }
}