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
