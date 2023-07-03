pipeline {
    
    agent any 
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        
        stage('Checkout'){
           steps {
                git 'https://github.com/MadanRaj09/todoAPP_django.git'
           }
        }

        stage('Build Docker'){
            steps{
                script{
                    sh '''
                    echo 'Buid Docker Image'
                    sudo docker build -t madan09/django_todo:$IMAGE_TAG .
                    '''
                }
            }
        }
          stage('run the container'){
           steps{
                script{
                    sh '''
                    echo 'starting the  container'
                    sudo docker run -d -p 8000:8000 --name todoapp madan09/django_todo:$IMAGE_TAG
                    '''
                }
            }
        }
         stage('Push the artifacts'){
           steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub1', variable: 'dockerhub')]) {
                    sh 'docker login -u madan09 -p ${dockerhub}'
}
                    sh '''
                    echo 'Push to docker hub'
                    docker push madan09/django_todo:${BUILD_NUMBER}
                    '''
                }
            }
        }
      }
   }
