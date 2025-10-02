pipeline {
  agent any
  stages {
    stage('scm checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/rajat1746/maven-project.git'
      }
    }

    stage('code build')
    {
      steps {
        withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
          sh 'mvn package'
        }
      }
    }

    stage('create docker image') {
      step {
        sh 'docker build -t rajatksingh/ethans954:v1.0'
      }
    }

    stage('push docker image to dockerhub') {
      steps {
        withDockerRegistry(credentialsId: 'DockerHubCredentials', url: 'rajatksingh/ethans954') {
          sh 'docker push rajatksingh/ethans954:v1.0 '
        }
      }
    }
  }
}
