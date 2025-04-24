pipeline {
    agent { label 'python' }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/michellemontoya/ejemplo-python.git', branch: 'main'
            }
        }

        stage('Instalar dependencias') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install --upgrade pip'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Ejecutar pruebas') {
            steps {
                // Ejecuta pytest y genera reporte en formato JUnit
                sh './venv/bin/pytest --junitxml=report.xml'
            }
        }

        stage('Publicar reporte') {
            steps {
                junit 'report.xml'
            }
        }
    }

    post {
        always {
            echo '✅ Pipeline completed.'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
