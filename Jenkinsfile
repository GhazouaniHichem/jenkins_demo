pipeline 
{
    tools {
        maven 'maven3.8.6'
    }

    agent { label 'Staging' }

    environment { NAME = "ghazouani" }

    parameters { string defaultValue: 'hichem', name: 'LASTNAME' }

    stages {

        stage ("Build") {
            steps {
                echo "hello $NAME ${params.LASTNAME}"
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

        
        
        
