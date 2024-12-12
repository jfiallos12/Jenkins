pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo "Clonando la rama ${env.BRANCH_NAME}"
                checkout scm
            }
        }
        stage('Build') {
            when {
                branch 'desarrollo'
            }
            steps {
                echo "Construyendo el proyecto desde la rama desarrollo"
                bat 'echo Compilación de desarrollo'
            }
        }
        stage('Test') {
            when {
                branch 'pruebas'
            }
            steps {
                echo "Ejecutando pruebas desde la rama pruebas"
                bat 'echo Ejecutando pruebas'
            }
        }
        stage('Deploy') {
            when {
                branch 'produccion'
            }
            steps {
                echo "Desplegando el proyecto desde la rama producción"
                bat 'echo Despliegue en producción'
            }
        }
        // Aquí agregamos la nueva etapa
        stage('Merge to Pruebas') {
    when {
        branch 'desarrollo'
    }
    steps {
        echo 'Fusionando cambios de desarrollo a pruebas...'
        bat '''
        git config user.name "Jenkins"
        git config user.email "jenkins@example.com"
        git checkout pruebas
        git merge desarrollo -m "Fusión automática desde desarrollo a pruebas"
        git push origin pruebas
        '''
    }
}
        stage('General') {
            steps {
                echo "Esta tarea se ejecuta en todas las ramas: ${env.BRANCH_NAME}"
                bat 'echo Tarea general para todas las ramas'
            }
        }
    }
    post {
        always {
            echo "Pipeline completado para la rama: ${env.BRANCH_NAME}"
        }
    }
}
