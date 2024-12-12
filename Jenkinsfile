pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo "Clonando la rama ${env.BRANCH_NAME}"
                checkout scm // Descarga el código de la rama activa
            }
        }
        stage('Build') {
            when {
                branch 'desarrollo' // Este paso se ejecuta solo en la rama desarrollo
            }
            steps {
                echo "Construyendo el proyecto desde la rama desarrollo"
                // Comandos específicos para compilar en desarrollo
                sh 'echo Compilación de desarrollo'
            }
        }
        stage('Test') {
            when {
                branch 'pruebas' // Este paso se ejecuta solo en la rama pruebas
            }
            steps {
                echo "Ejecutando pruebas desde la rama pruebas"
                // Comandos específicos para ejecutar pruebas
                sh 'echo Ejecutando pruebas'
            }
        }
        stage('Deploy') {
            when {
                branch 'produccion' // Este paso se ejecuta solo en la rama producción
            }
            steps {
                echo "Desplegando el proyecto desde la rama producción"
                // Comandos para el despliegue
                sh 'echo Despliegue en producción'
            }
        }
        stage('General') {
            steps {
                echo "Esta etapa se ejecuta en todas las ramas: ${env.BRANCH_NAME}"
                // Comandos generales que se ejecutan en todas las ramas
                sh 'echo Tarea general'
            }
        }
    }
    post {
        always {
            echo "Pipeline completado para la rama: ${env.BRANCH_NAME}"
        }
    }
}
