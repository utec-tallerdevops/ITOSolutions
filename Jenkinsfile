pipeline {
  
    agent none

    stages {
      
        stage('Login') {
         agent {
                node {
                    label 'master'
                }
            }
            steps {
                echo 'Ejecutando comando docker login devopsutec.azurecr.io -u devopsutec -p eYUZB+kRWGt19mj8Lj1RpbmSKnwdtw33...'
                sh 'docker login devopsutec.azurecr.io -u devopsutec -p eYUZB+kRWGt19mj8Lj1RpbmSKnwdtw33'
           }
        }
      
        stage('Construcción/Compilación de Imagenes en Master') {
            agent {
                node {
                    label 'master'
                }
            }
            steps {
                    echo 'Construcción/Compilación de Imagenes en Master...'
                   dir('worker'){ 
                     sh 'docker build devopsutec.azurecr.io/itosolutions-worker-1.0'
                     
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
                        sh 'docker push devopsutec.azurecr.io/itosolutions-worker-1.0:${BUILD_NUMBER}'
                        sh 'docker push devopsutec.azurecr.io/itosolutions-vote-1.0:${BUILD_NUMBER}'
                        sh 'docker push devopsutec.azurecr.io/itosolutions-result-1.0:${BUILD_NUMBER}'
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
