pipeline {
    agent any
    stages {
        stage('Merge to Pruebas') {
            steps {
                echo 'Intentando fusionar desarrollo a pruebas...'
                script {
                    bat '''
                    git config user.name "Jenkins"
                    git config user.email "jenkins@example.com"
                    git fetch origin desarrollo:desarrollo
                    git checkout pruebas
                    git merge desarrollo -m "Prueba de fusión"
                    git push origin pruebas
                    '''
                }
            }
        }
    }
    post {
        always {
            echo "Pipeline terminado para la rama ${env.BRANCH_NAME}"
        }
    }
}
