pipeline {
    agent any

    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                echo 'Clonando el código fuente desde el repositorio...'
                checkout scm
            }
        }

        stage('Checkout Desarrollo') {
            when {
                branch 'desarrollo'
            }
            steps {
                echo 'Clonando la rama desarrollo'
                script {
                    try {
                        bat '''
                        git config user.name "Jenkins"
                        git config user.email "jenkins@example.com"
                        git fetch origin
                        '''
                    } catch (Exception e) {
                        echo "Error en el checkout de desarrollo: ${e.message}"
                        error("Fallo en la etapa de Checkout Desarrollo")
                    }
                }
            }
        }

        stage('Build Desarrollo') {
            when {
                branch 'desarrollo'
            }
            steps {
                echo 'Construyendo el proyecto desde la rama desarrollo'
                script {
                    try {
                        bat '''
                        echo Compilación de desarrollo
                        '''
                    } catch (Exception e) {
                        echo "Error durante la compilación: ${e.message}"
                        error("Fallo en la etapa de Build Desarrollo")
                    }
                }
            }
        }

        stage('Test Pruebas') {
            when {
                branch 'pruebas'
            }
            steps {
                echo 'Ejecutando pruebas desde la rama pruebas'
                script {
                    try {
                        bat '''
                        echo Ejecutando pruebas
                        '''
                    } catch (Exception e) {
                        echo "Error en las pruebas: ${e.message}"
                        error("Fallo en la etapa de Test Pruebas")
                    }
                }
            }
        }

        stage('Deploy Producción') {
            when {
                branch 'produccion'
            }
            steps {
                echo 'Desplegando el proyecto desde la rama producción'
                script {
                    try {
                        bat '''
                        echo Despliegue en producción
                        '''
                    } catch (Exception e) {
                        echo "Error durante el despliegue: ${e.message}"
                        error("Fallo en la etapa de Deploy Producción")
                    }
                }
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
                        echo "Error durante el merge a pruebas: ${e.message}"
                        error("Fallo en la etapa de Merge to Pruebas")
                    }
                }
            }
        }

        stage('General Tasks') {
            steps {
                echo "Esta tarea se ejecuta en todas las ramas: ${env.BRANCH_NAME}"
                script {
                    try {
                        bat '''
                        echo Tarea general para todas las ramas
                        '''
                    } catch (Exception e) {
                        echo "Error en la tarea general: ${e.message}"
                        error("Fallo en la etapa de General Tasks")
                    }
                }
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