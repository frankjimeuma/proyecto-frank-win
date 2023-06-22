pipeline {
    agent any

    //Declaracion de valores de entorno
    environment {
        MESSAGE = "Curso de Intgracion Continua"
        LISTA_CORREOS = "franklin.jimenezumana@ucreativa"
        CUERPO_CORREO = "El pipeline ${BUILD_URL} tuvo un resultado"
        TITULO_CORREO = "${BUILD_URL} STATUS"
    }


  
    stages {
        stage('Bienvenida!') {
            steps {
                echo "Bienvenid@s al ${MESSAGE}, estamos corriendo en ${BUILD_URL} y este es el build ${BUILD_NUMBER} , also this is the node with name ${NODE_NAME} and Workspace ${WORKSPACE} in Jenkins location ${JENKINS_URL}"
            }
        }
      
        stage('Instalar dependencias') {
            steps {
                sh 'npm install'
            }
        }
            
        stage('Compilacion del APP') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Mostrar Archivos') {
            
            steps {
                sh 'pwd'
            }
        }
        stage('Despliegue Dev') {
            when {branch 'dev'}
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-dev/'
      
        
            }
        }
        stage('Despliegue Staging') {
            when {branch 'staging'}
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-staging/'
      
        
            }
        }

      stage('Despliegue Prod') {
            when {branch 'prod'}
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-prod/'
      
        
            }
        }
      stage('Failure') {
            steps {
                bat 'dir'
              
        
            }
        }
    }

      
    post {
      always {
          echo 'siempre me voy a ejecutar...no matter what happens in the world :| '
      }
      success {
          emailext body: "${CUERPO_CORREO} exitoso", subject: "${TITULO_CORREO}", to: "${LISTA_CORREOS}"
      }
      failure {
          emailext body: "${CUERPO_CORREO} fallido", subject: "${TITULO_CORREO}", to: "${LISTA_CORREOS}"
      }
      success {
          echo 'El ipeline da ok :)'
      }
      failure {
          echo 'Algo Salio Mal :('
      }
    
    }


      
    
}
