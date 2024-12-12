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
                bat 'echo Compilación de desarrollo' // Cambia `sh` por `bat`
            }
        }
        stage('Test') {
            when {
                branch 'pruebas'
            }
            steps {
                echo "Ejecutando pruebas desde la rama pruebas"
                bat 'echo Ejecutando pruebas' // Cambia `sh` por `bat`
            }
        }
        stage('Deploy') {
            when {
                branch 'produccion'
            }
            steps {
                echo "Desplegando el proyecto desde la rama producción"
                bat 'echo Despliegue en producción' // Cambia `sh` por `bat`
            }
        }
        stage('General') {
            steps {
                echo "Esta tarea se ejecuta en todas las ramas: ${env.BRANCH_NAME}"
                bat 'echo Tarea general para todas las ramas' // Cambia `sh` por `bat`
            }
        }
    }
    post {
        always {
            echo "Pipeline completado para la rama: ${env.BRANCH_NAME}"
        }
    }
}
