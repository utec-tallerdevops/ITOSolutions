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
       
                      sh 'ls'
                      sh 'cd result'
                      sh 'ls'
                     sh 'docker build devopsutec.azurecr.io/itosolutions-worker-1.0'
                 
   
       
                     sh 'docker build devopsutec.azurecr.io/itosolutions-vote-1.0'

                
                     sh 'docker build devopsutec.azurecr.io/itosolutions-result-1.0' 
               
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
