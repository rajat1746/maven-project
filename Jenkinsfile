pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/rajat1746/maven-project.git'
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
                    sh 'mvn package' // validate + compile + test + package
                }
            }
        }

        stage('code deploy')  // will deploy on target machine
        {
            steps { 
                
                sshagent(['tomcatid']) {
                    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.3.161:/usr/share/tomcat/webapps'
                }

             


                }
            }
        }


    }





