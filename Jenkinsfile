pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clonamos el repositorio
                git url: 'https://github.com/michellemontoya/ejemplo-python.git', branch: 'main'
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                sh '. /tmp/venv/bin/activate'
            }
        }




        stage('Install Dependencies') {
            steps {
                // Instalamos las dependencias en el entorno virtual
                sh '/tmp/venv/bin/pip install --upgrade pip'
                sh '/tmp/venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                // Ejecutamos las pruebas usando pytest y generamos el reporte
                sh '/tmp/venv/bin/pytest --junitxml=report.xml'
            }
        }

        stage('Archive Results') {
            steps {
                // Archivos de resultados de las pruebas
                junit 'report.xml'
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
