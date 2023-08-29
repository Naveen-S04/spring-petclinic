pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.2/bin:$PATH"
}
    stages {
        stage('Build Maven package') {
            steps {
                echo"-----------Build Started----------"
                sh '/usr/local/src/apache-maven/bin/mvn clean install'
                echo"----------Build completed--------"
            }
        }