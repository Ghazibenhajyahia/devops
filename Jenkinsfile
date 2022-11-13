pipeline{
    agent any

    stages{


        stage('Cloning from GitHub') {
                steps {
                    git branch: 'main', url: 'https://github.com/Ghazibenhajyahia/devops'
                }
                
            }
      
      stage('Clean Maven'){
            steps {
                sh 'mvn clean '
            }
            
        }
        stage('Compile Project'){
            steps {
                sh 'mvn compile  -DskipTests'
            }
            
        }
        
        
        /* stage('UNIT test'){
            steps{
                sh 'mvn test'
            }
        }*/

         stage('SonarQube Analysis'){
                steps {
                    sh """mvn sonar:sonar -DskipTests \
                            -Dsonar.language=java \
                          
                            
                    """
                }
                
            }
        
        
        
        
       stage('Nexus'){
            steps{
                sh 'mvn deploy -DskipTests'
            }
        }
        
        
        stage("Building Docker Image") {
                steps{
                    sh 'docker build -t ghazidev/achat .'
                }
        }
     
         stage("Login to DockerHub") {
                steps{
                   // sh 'sudo chmod 666 /var/run/docker.sock'
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u ghazidev -p Docker.Hub.147'
                }
        }
        stage("Push to DockerHub") {
                steps{
                    sh 'docker push ghazidev/achat'
                }
        }
    
               stage("Docker-compose") {
                steps{
                    sh 'docker-compose up -d'
                }
        }
    }
    
    post {
                success {
                   echo 'succes'
                }
failure {
                  echo 'failed'   
                }
             
       
    }
      

    }

