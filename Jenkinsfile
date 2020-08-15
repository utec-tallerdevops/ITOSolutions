pipeline {
  
    agent none

    stages {
        
        stage('Construcción/Compilación de Imagenes en Master') {
            agent {
                node {
                    label 'master'


                }
            }
            steps {
                    echo 'Construcción/Compilación de Imagenes en Master...'
                   dir('worker'){ 
                     sh 'docker build -t devopsutec.azurecr.io/itosolutions-worker-1.0'
                        }
                    dir('vote'){
                     sh 'docker build -t devopsutec.azurecr.io/itosolutions-vote-1.0'
                        }
                    dir('result'){
                     sh 'docker build -t devopsutec.azurecr.io/itosolutions-result-1.0' 
                        }
            }
        }

        stage('Push de Imagenes en Master') {
            agent {
                node {
                    label 'master'


                }
            }
            steps {
                    echo 'Push de Imagenes en Master...'
                    withDockerRegistry(credentialsId: 'ITOSolutions', url:'https://devopsutec.azurecr.io'){ 
                        sh 'docker push devopsutec.azurecr.io/itosolutions-worker-1.0'
                        sh 'docker push devopsutec.azurecr.io/itosolutions-vote-1.0'
                        sh 'docker push devopsutec.azurecr.io/itosolutions-result-1.0'
                    }
            }
        }

        stage('Verificacion') {
         agent {
                node {
                    label 'utec'
                }
            }
            steps {
                echo 'Ejecutando comando docker ps...'
                sh 'docker ps'
           }
        }

         stage('Deploy con docker-compose') {
         agent {
                node {
                    label 'utec'
                }
            }
            steps {
            withDockerRegistry(credentialsId: 'ITOSolutions', url:'https://devopsutec.azurecr.io'){ 
                echo 'Ejecutando deploy con docker-compose up -d...'
                sh 'docker-compose up -d'
                }
           }
        }

        stage('Verificacion Post docker-compose') {
         agent {
                node {
                    label 'utec'
                }
            }
            steps {
                echo 'Ejecutando comando docker ps...'
                sh 'docker ps'
                echo 'Ejecutando comando docker images...'
                sh 'docker images'
           }
        }

        stage('Docker Compose Down') {
         agent {
                node {
                    label 'utec'
                }
            }
            steps {
                echo 'Ejecutando comando docker-compose down...'
                sh 'docker-compose down'
           }
        }

        stage('Verificacion Final') {
         agent {
                node {
                    label 'utec'
                }
            }
            steps {
                echo 'Ejecutando comando docker ps...'
                sh 'docker ps'
                echo 'Ejecutando comando docker images...'
                sh 'docker images'
           }
        }

}

        }
