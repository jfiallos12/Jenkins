pipeline {
    agent any
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                echo 'Clonando el código fuente desde el repositorio...'
                checkout scm
            }
        }
        stage('Build Desarrollo') {
            steps {
                echo 'Construyendo el proyecto desde la rama desarrollo...'
                script {
                    try {
                        bat '''
                        echo Compilación de desarrollo exitosa
                        '''
                    } catch (Exception e) {
                        echo "Error durante la compilación: ${e.message}"
                        error("Fallo en la etapa de Build Desarrollo")
                    }
                }
            }
        }
        stage('Prueba básica') {
            steps {
                echo 'Pipeline sigue funcionando correctamente...'
            }
        }
    }
}
