pipeline {
    agent any

    environment {
        PYTHONUNBUFFERED = '1'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/michellemontoya/ejemplo-python.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Descargar e instalar pip si no está disponible
                sh 'curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py'  // Descargar el script para instalar pip
                sh 'python3 get-pip.py'  // Ejecutar el script para instalar pip
                sh 'python3 -m pip install --upgrade pip'  // Asegurarse de tener la versión más reciente de pip
                sh 'pip install pytest'  // Instalar pytest
            }
        }

        stage('Test') {
            steps {
                sh 'pytest --junitxml=report.xml'  // Ejecutar las pruebas y generar un reporte XML
            }
        }

        stage('Archive Results') {
            steps {
                junit 'report.xml'  // Archivar el reporte de pruebas
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
