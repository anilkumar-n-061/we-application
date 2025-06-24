pipeline{
    agent any
    
    tools{
        jdk 'java-11'
        maven 'maven'
    }
    
    stages{
        stage('Git-checkout'){
            steps{
                git branch: 'main' , url: 'https://github.com/anilkumar-n-061/we-application.git'
            }
        }
        stage('Code Compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Code Package'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Build and tag'){
            steps{
                sh 'docker build -t anilkumar-n-061/project-1 .'
            }
        }
        stage('Containerisation'){
            steps{
                sh '''
                docker run -it -d --name c8 -p 9008:8080 anilkumar-n-061/project-1
                '''
            }
        }
        stage('Login to Docker Hub') {
                    steps {
                        script {
                            withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                                sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                            }
                        }
                    }
        }
         stage('Pushing image to repository'){
            steps{
                sh 'docker push anilkumar-n-061/project-1'
            }
        }
        
    }
}
