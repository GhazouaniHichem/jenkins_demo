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

            
        }

        stage ("Test") {

            parallel {
                stage('TestA') {
                    steps {
                        echo "This is TEst A"
                    }
                    
                }

                stage('TestB') {
                    steps {
                        echo "This is TEst B"
                    }
            }
            post {
                success {
                    archiveArtifacts artifacts: "**/target/*.war"
                }
            }

        }


    }
    


}

        
        
        
