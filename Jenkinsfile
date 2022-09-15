pipeline 
{
    tools {
        maven 'maven3.8.6'
    }
    
    agent { label 'Staging' }

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

        
        
        
