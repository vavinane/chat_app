pipeline {
    agent any
    environment {
        PROJECT_ID = 'homedepot-342320'
        LOCATION = 'us-east1-c'
        CREDENTIALS_ID = 'homedepot-342320'
        CLUSTER_NAME = 'homedepot-342320-gke'
    } 
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Package") {
            steps {
                sh "/usr/local/bin/mvn clean package"
            }
        }
        stage("Dockerize") {
            steps {
                sh "/usr/local/bin/docker build -t studentapp ."
            }
        }
        stage("Authenticate Artifact") {
            steps {
                sh "/usr/local/bin/gcloud auth configure-docker northamerica-northeast2-docker.pkg.dev"               
            }
        }
        stage("Docker Tag") {
            steps {
                sh "docker tag my-app northamerica-northeast2-docker.pkg.dev/homedepot-342320/gcp-artifactory/chatapp:v1"               
            }
        }
        stage("Docker Push") {
            steps {
                sh "docker push northamerica-northeast2-docker.pkg.dev/homedepot-342320/gcp-artifactory"               
            }
        }
    }   
}
