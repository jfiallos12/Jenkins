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
                echo 'Pipeline en desarrollo ejecutándose correctamente después del checkout...'
            }
        }
    }
}
