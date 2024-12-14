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
                echo 'Construyendo el proyecto en desarrollo...'
                bat '''
                echo Compilación de desarrollo
                '''
            }
        }

        stage('Merge to Pruebas') {
            timeout(time: 5, unit: 'MINUTES') { // Establece un timeout de 5 minutos
                steps {
                    echo 'Fusionando cambios de desarrollo a pruebas...'
                    script {
                        withCredentials([usernamePassword(credentialsId: 'github-credentials-id', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_TOKEN')]) {
                            bat '''
                            echo Configurando credenciales de Git...
                            git config user.name "%GIT_USER%"
                            git config user.email "jenkins@example.com"

                            echo Obteniendo cambios desde desarrollo...
                            git fetch origin desarrollo:desarrollo

                            echo Realizando checkout a la rama pruebas...
                            git checkout pruebas

                            echo Realizando merge de desarrollo a pruebas...
                            git merge desarrollo -m "Fusión automática desde desarrollo a pruebas"

                            echo Enviando cambios a la rama pruebas...
                            git push https://%GIT_USER%:%GIT_TOKEN%@github.com/jfiallos12/Jenkins.git pruebas
                            echo Push completado.
                            '''
                        }
                    }
                }
            }
        }

        stage('General Tasks') {
            steps {
                echo "Esta tarea se ejecuta en todas las ramas: ${env.BRANCH_NAME}"
                bat '''
                echo Tarea general para todas las ramas
                '''
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
