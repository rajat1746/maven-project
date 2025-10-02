pipeline {
  agent any

  stages {
    stage('SCM Checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/rajat1746/maven-project.git'
      }
    }

    stage('Build with Maven') {
      steps {
        withMaven(jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') {
          sh 'mvn clean package'
        }
      }
    }

    stage('Create Docker Image') {
      steps {
        sh 'docker build -t rajatksingh/ethans954:v1.0 .'
      }
    }

    stage('Push Docker Image to DockerHub') {
      steps {
        withDockerRegistry(credentialsId: 'DockerHubCredentials', url: 'https://index.docker.io/v1/') {
          sh 'docker push rajatksingh/ethans954:v1.0'
        }
      }
    }
  }
}
