stage('Test') {
  steps {
    echo 'We are Starting the Testing'
  }
}
stage('init') {
  checkout scm
}
stage('Build') {
  steps {
    echo 'Packaging the app into jars with maven'
    sh 'mvn clean package'
  }
}
stage('Copy the war to Tomcat') {
  steps {
    echo "Copy to Staging Area"
    sh 'scp /var/lib/jenkins/workspace/deploy_on_tomcat-server/webapp/target/*.war ec2-user@3.92.4.84://opt/tomcat/webapps'
  }
}
