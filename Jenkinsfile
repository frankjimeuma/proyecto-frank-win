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
            //when {branch 'dev'}
            steps {
                sh 'pwd'
            }
        }
        stage('Despliegue') {
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-dev/'
      
        
            }
        }
        stage('Despliegue') {
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-staging/'
      
        
            }
        }
      stage('Despliegue') {
            steps {
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/franklin-prod/'
      
        
            }
        }
    }
}
