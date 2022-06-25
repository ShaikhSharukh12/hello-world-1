pipeline {
    agent any
    environment {
        PATH=  "/opt/maven/apache-maven-3.8.6/bin:$PATH"
    }
    stages {
        stage('git') {
            steps {
                git credentialsId: 'Jenkinspipeline', url: 'https://github.com/ShaikhSharukh12/hello-world-1.git'
            }
        }
        stage('Build code') {
            steps {
                sh "mvn clean install"
            }
        }
       stage('Deploy code') {
            steps {
                sshagent(['host-server']) {
                  sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipeline_project/webapp/target/webapp.war ec2-user@3.142.230.18:/opt/apache-tomcat-8.5.81/webapps"

                }
            }
        }
    }
}
