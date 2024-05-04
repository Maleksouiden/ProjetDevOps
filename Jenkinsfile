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
    }
    post {
        /*success {
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
        }*/
        always {
            cleanWs()
        }
    }
    
}
