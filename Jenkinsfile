pipeline {
    agent any
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                echo 'Clonando el código fuente desde el repositorio...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Construyendo el proyecto en desarrollo...'
                bat '''
                echo Compilación de desarrollo
                '''
            }
        }
        stage('Merge to Pruebas') {
            steps {
                echo 'Fusionando cambios de desarrollo a pruebas...'
                bat '''
                git config user.name "Jenkins"
                git config user.email "jenkins@example.com"
                git fetch origin desarrollo:desarrollo
                git checkout pruebas
                git merge desarrollo -m "Fusión automática desde desarrollo a pruebas"
                git push origin pruebas
                '''
            }
        }
    }
    post {
        always {
            echo "Pipeline completado para la rama: desarrollo"
        }
        success {
            echo "Pipeline finalizado con éxito."
        }
        failure {
            echo "Pipeline fallido."
        }
    }
}
