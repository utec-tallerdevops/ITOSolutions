
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

        stage('Pruebas') {
            steps {
                echo 'Probando cosas...'
            }
        }
      stage('Pruebas Docker PS') {
            steps {
                echo 'Probando comando docker ps...'
                sh 'docker ps'
                echo 'Probando comando docker ps -a...'
                sh 'docker ps'
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

