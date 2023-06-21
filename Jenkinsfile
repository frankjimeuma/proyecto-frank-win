pipeline {
    agent any
//hello
    stages {
        
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
        stage('Despliegue1') {
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-dev/'
      
        
            }
        }
        stage('Despliegue2') {
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-staging/'
      
        
            }
        }
      stage('Despliegue3') {
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-prod/'
      
        
            }
        }
    }
}