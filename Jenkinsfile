pipeline {
    agent any

    stages {
        stage('Checkout GIT') {
            steps {
                echo 'Pulling ... ';
                git branch: 'main',
                url : 'https://github.com/Ghazibenhajyahia/SpringAOP.git'
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
        
        stage('SonarQube Analysis'){
                steps {
                    sh """mvn sonar:sonar -DskipTests \
                            -Dsonar.language=java \
                          
                            
                    """
                }
                
            }
    }
}
