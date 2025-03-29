pipeline {
    agent any

    stages {
        stage('git scm checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/harshaldhangar7/maven-project.git'
            }
        }
    stage('validate') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                sh 'mvn validate'
}
            }
        }
    stage('package') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                sh 'mvn clean package'
}
            }
        }
    }

}