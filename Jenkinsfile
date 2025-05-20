pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/kumargaurav039/maven-project.git'
            }
        }
        stage('code validate')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn validate' // validate the code
                }
            }
        }
        stage('code compile')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn compile' // compile
                }
            }
        }
        stage('code test')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn test' // test
                }
            }
        }
        stage('code build')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    withSonarQubeEnv(credentialsId: 'sonar', installationName: 'sonar') {
                        sh 'mvn package sonar:sonar'
                    }
                }
            }
        }
    }
}