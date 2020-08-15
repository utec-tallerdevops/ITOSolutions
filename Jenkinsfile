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
                    sh 'docker build -t devopsutec.azurecr.io/itosolutions-worker-1.0:${BUILD_NUMBER} .'
                  }
              
                dir('vote'){ 
                    sh 'docker build -t devopsutec.azurecr.io/itosolutions-vote-1.0:${BUILD_NUMBER} .'
                  }
              
                dir('result'){ 
                    sh 'docker build -t devopsutec.azurecr.io/itosolutions-result-1.0:${BUILD_NUMBER} .'
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


    }

        }
