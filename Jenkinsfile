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
                    docker build -t madan09/django_todo:${BUILD_NUMBER} .
                    '''
                }
            }
        }
          stage('run the container'){
           steps{
                script{
                    sh '''
                    echo 'starting the  container'
                    docker run -d -p 8000:8000 madan09/django_todo:${BUILD_NUMBER}
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    sh '''
                    echo 'Push to Repo'
                    docker push madan09/django_todo:${BUILD_NUMBER}
                    '''
                }
            }
        }
     }
  }
