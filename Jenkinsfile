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
       
                     sh 'docker build devopsutec.azurecr.io/itosolutions-worker-1.0'
   
       
                     sh 'docker build -t devopsutec.azurecr.io/itosolutions-vote-1.0'

                
                     sh 'docker build -t devopsutec.azurecr.io/itosolutions-result-1.0' 
               
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


    }

        }
