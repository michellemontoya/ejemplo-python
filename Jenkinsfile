pipeline {
    agent any

    environment {
        PYTHONUNBUFFERED = '1'
    }

    stages {
        stage('Checkout') {
            steps {
                // Asegúrate de usar el repositorio correcto
                git url: 'https://github.com/michellemontoya/ejemplo-python.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Asegurarse de que pip esté disponible
                sh 'python3 -m ensurepip --upgrade'  // Instalar pip si no está presente
                sh 'python3 -m pip install --upgrade pip'  // Actualizar pip
                sh 'pip install pytest'  // Instalar pytest
            }
        }

        stage('Test') {
            steps {
                // Ejecutar las pruebas
                sh 'pytest --junitxml=report.xml'  // Ejecutar pruebas y generar reporte XML
            }
        }

        stage('Archive Results') {
            steps {
                // Archivar el reporte de pruebas
                junit 'report.xml'  // Archivar resultados de las pruebas
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
