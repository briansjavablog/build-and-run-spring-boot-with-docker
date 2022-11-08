pipeline{
    agent any
    stages{
        stage("Prepare environment"){
            steps{
                load "version.groovy"
                currentBuild.name = "${env.MAJOR_VERSION}.${env.MINOR_VERSION}.${env.BUILD_NUMBER}"
            }
        }
        stage("Build application"){
            steps{
                skaffold build
            }
        }
        stage("Deploy application"){
            steps{
                skaffold run
            }
        }
    }
}