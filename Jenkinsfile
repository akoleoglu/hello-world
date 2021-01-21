pipeline {
    agent { label "master" }
    stages {
        stage('Test') {
            steps {
                echo 'We are Starting the Testing'
            }
        }   
        stage('Checks out java source from a github project') {
            steps {
                echo "checkout scm"
                echo ' [ -f ./*.war ] && echo "This file exists!"'
            }
        }
        stage('Builds the code') {
            steps {
                echo 'Packaging the app into jars with maven'
                echo 'mvn clean package'
            }
        }
        stage('Copies the war file to a deployment server') {
            steps {
                echo "Copy to war to Tomcat "
                echo 'scp /var/lib/jenkins/workspace/deploy_on_tomcat-server/webapp/target/*.war ec2-user@3.92.4.84:/opt/tomcat/webapps'
            }
        }
        stage('Tests an endpoint to see if the server is up') {
            steps {
            echo "Check if the tomcat app is ready or not"
            echo '''
            script {
                while(true) {
                    try{
                        sh "curl -s --connect-timeout 60 3.92.4.84:8080"
                        echo "Tomcat server is ready."
                        break
                    }
                    catch(Exception){
                        echo "Could not connect to Tomcat - it is not ready yet."
                        sleep(5)
                    }
                }'''
            }
        }
        stage('Runs integration tests') {
            steps {
                echo "Runs integration tests"
                echo 'mvn verify'
            }
        }
    }
    post {
        always {
            echo 'Deleting war file'
            echo 'rm -rf ec2-user@3.92.4.84:/opt/tomcat/webapps/*.war'
            }
        }
}

