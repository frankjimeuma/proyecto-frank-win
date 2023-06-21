pipeline {
    agent any

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
                sh 'cd dist || ls -la'
            }
        }
    }
}
