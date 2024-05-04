pipeline {
     agent any
    stages {
       stage("Go to Project") {
            steps {
                sh "cd gestion-station-ski/"
            }
        }
        stage("Build Project") {
            steps {
                sh "mvn clean install -DskipTests"
            }
        }
            stage('Connection to Nexus') {
          steps {
            sh "sudo docker login -u admin -p admin 192.168.33.10:8081"
            }
          }
        stage('Push jar to maven repo'){
            steps{
                sh'mvn clean deploy -DskipTests'
            }
        }
        stage('Get jar from maven repo'){
            steps{
                 sh "wget -O app.jar  http://192.168.2.80:8081/repository/maven-releases app.jar"
            }
        } 
        stage('Build Docker image') {
          steps {
               sh "sudo docker build  --build-arg JAR_FILE=app.jar -t ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ."
          }
        }
        stage('Push Docker image to dockerhub') {
          steps {
            sh "sudo docker push ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}" 
            }
          }
        stage('Get Docker image from dockergub') {
          steps {
            sh "sudo docker pull ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}" 
            }
        }
        stage('Shutdown APP with compose'){
          steps{
            sh 'sudo docker-compose down -v'
          }
        }
        stage('Run app with compose'){
          steps{
            sh 'sudo docker-compose up -d'
          }
        }
    }
    post {
        success {
            emailext body: "The pipeline has completed successfully",
                attachLog: true,
                subject: "Jenkins pipeline completed successfully",
                to: "malek.souiden@esprit.tn"
        }
        failure {
            emailext body: "The pipeline has failed",
                attachLog: true,
                subject: "Jenkins pipeline failed",
                to: "malek.souiden@esprit.tn"
        }
        always {
            cleanWs()
        }
    }
    
}
