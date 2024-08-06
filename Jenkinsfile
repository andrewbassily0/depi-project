pipeline{
    
    agent any
    
    stages{
        
        stage('build'){

          steps{

            sh "docker build -t andrewbassily0/depi-project:v${env.BUILD_NUMBER} ./Docker-Task/"
            withCredentials([usernamePassword(credentialsId: 'myDockerHub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                sh "docker login -u $user -p $pass"
            }
            sh "docker push andrewbassily0/depi-project:v${env.BUILD_NUMBER}"
          }            
        }
        
        stage('deploy'){

          steps{

            sh "docker run -d -p 400${env.BUILD_NUMBER}:8080 --name cont_build_${env.BUILD_NUMBER} andrewbassily0/depi-project:v${env.BUILD_NUMBER}"
          }     
        }
    }
}
