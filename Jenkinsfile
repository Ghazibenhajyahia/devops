pipeline{
    agent any

    stages{


        stage('Cloning from GitHub') {
                steps {
                    git branch: 'main', url: 'https://github.com/Ghazibenhajyahia/devops'
                }
                
            }
        stage('MVN COMPILE') {
                  steps {
                     sh 'mvn compile'
                 }
              }
                stage('mvn Test') {
                  steps {
                     sh 'mvn test'
                  }
              }
                stage('mvn Verify') {
                   steps {
                     sh 'mvn verify'
                }
             }

         stage('SonarQube Analysis'){
                steps {
                    sh "mvn sonar:sonar \
                           -Dsonar.projectKey=sonar \
                           -Dsonar.host.url=http://192.168.33.10:9000 \
                           -Dsonar.login=092bfe111b6a8e26f3dacd0d45543eb5bd1b8af3"
                }
                
            }
                stage('mvn clean package') {
                               steps {
                                 sh 'mvn clean package'
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
      
    }
