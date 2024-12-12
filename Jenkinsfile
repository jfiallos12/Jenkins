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
            when {
                branch 'desarrollo'
            }
            steps {
                echo 'Fusionando cambios de desarrollo a pruebas...'
                script {
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

        stage('General Tasks') {
            steps {
                echo "Esta tarea se ejecuta en todas las ramas: ${env.BRANCH_NAME}"
                script {
                    bat '''
                    echo Tarea general para todas las ramas
                    '''
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
