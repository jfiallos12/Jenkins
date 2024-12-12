pipeline {
    agent any
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                echo 'Clonando el código fuente desde el repositorio...'
                checkout scm
            }
        }
        stage('Merge to Pruebas') {
            steps {
                echo 'Fusionando cambios de desarrollo a pruebas...'
                script {
                    try {
                        bat '''
                        git config user.name "Jenkins"
                        git config user.email "jenkins@example.com"
                        git fetch origin desarrollo:desarrollo
                        git checkout pruebas
                        git merge desarrollo -m "Fusión automática desde desarrollo a pruebas"
                        git push origin pruebas
                        '''
                    } catch (Exception e) {
                        echo "Error durante el merge: ${e.message}"
                        error("Fallo en la etapa de Merge to Pruebas")
                    }
                }
            }
        }
    }
    post {
        always {
            echo "Pipeline completado para la rama: ${env.BRANCH_NAME}"
        }
    }
}
