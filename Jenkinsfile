pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}
    stages {
        stage('Build Maven package') {
            steps {
                echo"-----------Build Started----------"
                sh sh './mvnw package'

                echo"----------Build completed--------"
            }
        }
    }
}
