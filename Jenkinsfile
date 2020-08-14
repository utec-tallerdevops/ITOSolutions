pipeline {
  
    agent none

    stages {
        
        stage('Construccion') {
            agent {
                node {
                    label 'master'


                }
            }
            steps {
                    echo 'Construyendo en master...'
                    sh 'uname -a'
            }
        }

      stage('Verificacion') {
         agent {
                node {
                    label 'master'
                }
            }
            steps {
                echo 'Ejecutando comando docker ps...'
                sh 'docker ps'
                echo 'Ejecutando comando docker ps -a...'
                sh 'docker ps -a'
                echo 'Ejecutando comando ls...'
                sh 'ls'
           }
        }


        stage('Docker Compose') {
         agent {
                node {
                    label 'master'
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
                    label 'master'
                }
            }
            steps {
                echo 'Ejecutando comando docker ps...'
                sh 'docker ps'
                echo 'Ejecutando comando docker ps -a...'
                sh 'docker ps -a'
           }
        }
/*
        stage('Despliegue en agente UTEC'){
            agent {
                node {
                    label 'utec'
                }
            }
            steps{
                 echo 'Desplegando en agente UTEC...'
                 sh 'uname -a'
            }
        }
*/
    
    }

}
