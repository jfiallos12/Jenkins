pipeline {
    agent any

    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                echo 'Clonando el código fuente desde el repositorio...'
                checkout scm
            }
        }

        stage('Prueba básica') {
            steps {
                echo 'Probando ejecución básica en el pipeline de desarrollo...'
            }
        }
    }

    post {
        always {
            echo "Pipeline básico completado para la rama: ${env.BRANCH_NAME}"
        }
    }
}
