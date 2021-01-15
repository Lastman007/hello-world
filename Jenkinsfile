#!groovy

pipeline {
    agent any
    environment {
        PATH = "/opt/apache-maven-3.6.3/bin:$PATH"
    }


    stages {
        stage("copy the code to local repo") {
            steps {
                git credentialsId: 'git_credentials', branch: 'homepage', url: 'https://github.com/Lastman007/hello-world.git'
            }
        }
        stage("build code"){
            steps{
              sh "mvn clean install"
            }
        }
        stage("deploy"){
            steps{
              sshagent(['deploy_user']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@18.207.99.170:/opt/apache-tomcat-8.5.61/webapps"
                 
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
