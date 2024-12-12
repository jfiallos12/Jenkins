pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Clonando el código fuente...'
                checkout scm
            }
        }
        stage('Merge to Pruebas') {
            steps {
                script {
                    try {
                        // ... (tu código existente)
                        echo "Verificando estado del repositorio..."
                        sh 'git status'
                        echo "Realizando la fusión..."
                        sh 'git merge desarrollo -m "Fusión automática"'
                        // Manejar conflictos si es necesario
                        sh 'git push origin pruebas'
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