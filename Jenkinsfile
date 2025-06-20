pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/kumargaurav039/maven-project.git'
            }
        }
        stage('compile the job') //validate then compile
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn validate'
                }
            }
        }
        stage('compile the code') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn compile'
                }
            }
        }
        stage('package the code') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn clean package'
                }
            }
        }
        stage('create docker image') {
            steps {
                sh 'docker build -t kubharshal/docker_cicd:latest .'
            }
        }
        stage('push docker image to dockerhub') {
            steps {
                
                withDockerRegistry(credentialsId: 'docker_cicd', url: 'https://index.docker.io/v1/') {
                    sh 'docker push kubharshal/docker_cicd:latest'
                }
            }
        }
    }
}
//sh 'scp -o StrictHostkeyCheking=no webapp/target/webapp.war ec2-user@172.31.11.185:/usr/share/tomcat/webapps'