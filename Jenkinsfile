pipeline {
    agent any
    stages {
        stage('Build Application') {
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn clean package'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh 'chmod +x deliver-script.sh'
                sh './deliver-script.sh'
            }
        }
    }
}
