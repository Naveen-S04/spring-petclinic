pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"



    
        docker_image="spring-petclinic"
        docker_tag="${env.BUILD_ID}"
        source="${WORKSPACE}/Dockerfile"
        destination="/home/ubuntu/.m2/repository/org/springframework/samples/spring-petclinic/3.1.0-SNAPSHOT/spring-petclinic-3.1.0-SNAPSHOT.jar"
        DOCKER_PASSWORD=credentials('Dockerlogin')
        dockerhub_repo="naveens04"
        DOCKER_USERNAME="naveens04"
    
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
                sh 'sudo su - cp -p ${source} ${destination}'
                sh 'sudo su  - cd ${destination}; sudo docker build -t ${docker_image}:${docker_tag} .'
            }
        }
        
        stage('Dockerhub login') {
            steps {
                sh 'echo $DOCKER_PASSWORD |sudo docker login -u $DOCKER_USERNAME --password-stdin'
            }
        }

        stage('Push docker image') {
            steps {
                sh 'sudo docker tag ${docker_image}:${docker_tag} ${dockerhub_repo}/${docker_image}:${docker_tag}'
                sh 'sudo docker push ${dockerhub_repo}/${docker_image}:${docker_tag}'
            }
        }
    }
}
