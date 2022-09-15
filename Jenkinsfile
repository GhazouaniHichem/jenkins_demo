pipeline 
{
//maven3.8.6
    //agent { label 'Staging' }
    agent any
    stages {

        stage ("Build") {
            steps {
                sh 'mvn clean package'
            }

            post {
                success {
                    archiveArtifacts artifacts: "**/target/*.war"
                }
            }
        }


    }
    


}

        
        
        
