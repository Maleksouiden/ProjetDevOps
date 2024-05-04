pipeline {
     environment {
  
      
    }
    stages {
        stage("Build Project") {
            steps {
                sh "mvn clean package -DskipTests"
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
        /*always {
            cleanWs()
        }*/
    }
    
}
