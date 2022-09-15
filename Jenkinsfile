pipeline 
{
    tools {
        maven 'maven3.8.6'
    }

    agent { label 'Staging' }

    environment { NAME = "ghazouani" }

    parameters { 
        string defaultValue: 'hichem', name: 'LASTNAME' 
        choice choices: ['dev', 'prod'], name: 'select_environment'
        }

    stages {

        stage ("Build") {
            steps {
                echo "hello $NAME ${params.LASTNAME}"
                sh 'mvn clean package -DskipTests=true'
            }

            
        }

        stage ("Test") {

            parallel {
                stage('TestA') {
                    agent { label 'Staging' }
                    steps {
                        echo "This is TEst A"
                        sh "mvn test"
                    }
                    
                }

                stage('TestB') {
                    agent { label 'Staging' }
                    steps {
                        echo "This is TEst B"
                        sh "mvn test"
                    }
                }
                
            }
            post {
                    success {
//                        archiveArtifacts artifacts: "**/target/*.war"
                        dir("webapp/target/")
                        {
                            stash name: "maven-build", includes: "*.war"
                        }
                    }
                }

        }

        stage ('Deploy dev') {

            when { expression {params.select_environment == 'dev'} 
                beforeAgent true
            }

            agent { label 'Staging' }

            steps {
                dir("/var/www/html")
                {
                    unstash "maven-build"
                }

                sh """
                cd /var/www/html/
                jar -xvf webapp.war
                """
            }
        }


    }
    


}

        
        
        
