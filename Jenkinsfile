pipeline{
    agent any
    tools{
        maven 'M3'
    }
    stages{
        stage('Cleaning workspace'){
            steps{
                sh 'echo "---=--- Cleaning Stage ---=---"'
                sh 'mvn clean'
                script{
                    try {
                    sh 'docker stop myboot && docker rm myboot'
                } catch (Exception e){
                    echo '---=--- no container to remove ---=---'
                }
                    
                }
                
            }
            
        }
        stage('Checkout'){
            steps{
                sh 'echo "---=--- Checkout ---=---"'
                git branch: 'master', url:'https://github.com/mathildalandreau/SimpleBoot.git'
                
            }
            
        }
        stage('Compile'){
            steps{
                sh 'echo "---=--- Compile ---=---"'
                sh 'mvn clean compile'
            }
            
        }
        stage('Test'){
            steps{
                sh 'echo "---=--- Test ---=---"'
                sh 'mvn test'
            }
            
        }
        stage('Package'){
            steps{
                sh 'echo "---=--- Package ---=---"'
                sh 'mvn package -DskipTests'
            }
            
        }
        stage('Docker'){
            steps{
                sh 'echo "---=--- Docker ---=---"'
                sh 'docker build -t mathildalandreau/myboot:1.0 .'
            }
            
        }
        stage('Deploy to local'){
            steps{
                sh 'echo "---=--- Deploy to local ---=---"'
                sh 'docker run -d --name myboot -p 8180:8180 mathildalandreau/myboot:1.0'
            }
            
        }
        
    }
}