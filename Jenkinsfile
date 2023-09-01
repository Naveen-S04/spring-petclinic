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
<<<<<<< HEAD
                sh sh './mvnw package'
=======
                sh 'mvn clean install'
>>>>>>> 1ad3ae5090e421fd5320307cb05ab43ba94eff31
                echo"----------Build completed--------"
            }
        }
    }
}
