pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Clonando el código fuente desde el repositorio...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Construyendo el proyecto desde la rama desarrollo'
                bat 'echo Compilación exitosa'
            }
        }

        stage('Merge to Pruebas') {
            when {
                branch 'desarrollo'
            }
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

        stage('General Tasks') {
            steps {
                echo "Tarea general para la rama: ${env.BRANCH_NAME}"
                bat 'echo Ejecutando tareas generales'
            }
        }
    }

    post {
        always {
            echo "Pipeline completado para la rama: ${env.BRANCH_NAME}"
        }
        success {
            echo "Pipeline finalizado con éxito para la rama: ${env.BRANCH_NAME}"
        }
        failure {
            echo "Pipeline fallido en la rama: ${env.BRANCH_NAME}"
        }
    }
}
