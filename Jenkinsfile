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
                // Crear un entorno virtual
                sh 'python3 -m venv venv'  // Crea un entorno virtual llamado 'venv'
                sh '. venv/bin/activate'   // Activa el entorno virtual
                sh 'pip install --upgrade pip'  // Asegurarse de tener pip actualizado en el entorno virtual
                sh 'pip install pytest'  // Instalar pytest dentro del entorno virtual
            }
        }

        stage('Test') {
            steps {
                sh '. venv/bin/activate && pytest --junitxml=report.xml'  // Ejecutar pruebas dentro del entorno virtual
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
