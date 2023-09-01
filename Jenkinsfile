pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"



        dockerhub_repo="naveens04"
        docker_image="dockerspringpet"
        
        source="${WORKSPACE}/Dockerfile"
        destination="/home/ubuntu/.m2/repository/org/springframework/samples/spring-petclinic/3.1.0-SNAPSHOT/"
        DOCKERHUB_CREDENTIALS = credentials('Dockerlogin')
       
        
    
}
    stages {
        stage('Build Maven package') {
            steps {
                echo"-----------Build Started----------"
                sh 'mvn clean install -DskipTests'
                echo"----------Build completed--------"
            }
        }

          stage('Build docker image') {
            steps {
                echo"-----------Build Started for Docker Image---------"
              
                sh 'cp -p ${source} ${destination}'
                sh 'cd ${destination}; sudo docker build -t ${docker_image}:v1 .'
            

                echo"-----------Build Ended for Docker Image----------"
            }
        }
        
       

        stage('Dockerhub login') {
            steps {

                 echo"-----------Docker hub login----------"
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                 echo"-----------Docker hub login step ended----------"
            }
        }

       stage('Push docker image') {
            steps {
                                sh 'sudo docker tag ${docker_image}:v1 ${dockerhub_repo}/${docker_image}:$v1'

                sh 'sudo docker push ${dockerhub_repo}/${docker_image}:v1'
            }
        }
    }
}
