pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/AryanKulathinal/project1-service-registry.git', branch: 'main'
            }
        }
        stage('Pre_Build'){
            steps {
                bat "docker rm -f registry_container"
                bat "docker rmi -f registry_image"
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {

                bat "docker build -t registry_image ."
                bat "docker run -p 8761:8761 -d --name registry_container registry_image"
            }
        }
    }
}
