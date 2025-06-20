pipeline {
    agent any
    stages {
        // Continuous Integration (CI)
        stage('git scm checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/harshaldhangar7/maven-project.git'
            }
        }
        stage('validate the code') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn validate'
                }
            }
        }
        stage('compile the job') //validate then compile
        {
            steps {
               withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn compile'
                }
            }
        }
        stage('execute unit test framework') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn test'
                }
            }
        }
        stage('build the code') {
            steps {
               withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn clean -B -DskipTests package'
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