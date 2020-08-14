pipeline {
  
    agent none

    stages {
        
        stage('Construccion') {
            agent {
                node {
                    label 'utec'


                }
            }
            steps {
                    echo 'Construyendo en agente UTEC...'
                    sh 'uname -a'
            }
        }

        
      stage('Login') {
         agent {
                node {
                    label 'utec'
                }
            }
            steps {
                echo 'Ejecutando comando docker login devopsutec.azurecr.io -u devopsutec -p eYUZB+kRWGt19mj8Lj1RpbmSKnwdtw33...'
                sh 'docker login -u devopsutec -p eYUZB+kRWGt19mj8Lj1RpbmSKnwdtw33'
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


        stage('Docker Compose') {
         agent {
                node {
                    label 'utec'
                }
            }
            steps {
                echo 'Ejecutando docker-compose up -d...'
                sh 'docker-compose up -d'
           }
        }

         stage('Verificacion Post Compose') {
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


         stage('Verificacion Post Compose Down') {
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


         stage('Parar y Remover Contenedores') {
         agent {
                node {
                    label 'utec'
                }
            }
            steps {
                echo 'Ejecutando comando docker stop $(docker ps -a -q)...'
                sh 'docker stop $(docker ps -a -q)'
                echo 'Ejecutando comando docker rm $(docker ps -a -q)'
                sh 'docker rm $(docker ps -a -q)'
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