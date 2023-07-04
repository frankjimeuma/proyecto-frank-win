pipeline {
    agent {
	label 'linux-agent'
	}   
    

    //Declaracion de valores de entorno
    environment {
        MESSAGE = "Curso de Intgracion Continua"
        LISTA_CORREOS = "franklin.jimenezumana@ucreativa"
        CUERPO_CORREO = "El pipeline ${BUILD_URL} tuvo un resultado"
        TITULO_CORREO = "${BUILD_URL} STATUS"
        AWS_ACCESS_KEY_ID=credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY=credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION='us-east-1'
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
      
        //stage('Correr pruebas de unidad') {
           // steps {
                //sh 'npm run test'
            //}
        //}  
      
        stage('Compilacion de la aplicacion Angular') {
            steps {
                sh 'npm run build'
            }
        }
        

        stage('Mostrar Archivos') {
            steps {
                //the following command works with Windows
                //sh 'dir dist'

                //the following command works with linux
                sh 'ls dist'
            }
        }
        stage('Deploy to server Development') {
            when {branch 'development'}
            steps {
                // the following line is for Dev in Digital Ocean for Linux agent
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-dev/'
      
        
            }
        }
        stage('Deploy to server Staging') {
            when {branch 'staging'}
            steps {
                // the following line is for Staging in Digital Ocean for Linux agent
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-staging/'
      
        
            }
        }

      stage('Deploy to server Production') {
            when {branch 'production'}
            steps {
                //the following line is for Prod  in Digital Ocean for Linux agent
                //sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-prod/'
                //bat 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-prod/'

                //the following line is for Prod deploy in AWS S3 bucket Linux agent
                sh 'aws s3 cp dist/angular-app/ s3//proyecto-frank-s3 --recursive'
                
        
            }
        }
      stage('success') {
            steps {
                sh 'ls -la'
              
        
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
 //     success {
   //       echo 'El ipeline da ok :)'
     // }
      //failure {
        //  echo 'Algo Salio Mal :('
      //}
    
    }


      
    
}
