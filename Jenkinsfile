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
        // CD (Continuous Deployment) - Deploy the code to Devlop environment
        stage('Deploy the code on Tomcat Server') {
            steps {
                sshagent(['DEVCICD']) {
                    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.11.185:/usr/share/tomcat/webapps'
                }
            }
        }
    }
}
//sh 'scp -o StrictHostkeyCheking=no webapp/target/webapp.war ec2-user@172.31.11.185:/usr/share/tomcat/webapps'