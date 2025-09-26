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
       stage('code deploy') 
    {
      steps {
      sshagent(['DEVCICD']){
       sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.38.208:/user/share/tomact/webapps'
        }
      }
      }
    }
    }
  

