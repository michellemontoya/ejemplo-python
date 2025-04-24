pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/michellemontoya/ejemplo-python.git', branch: 'main'
            }
        }

        stage('Create Virtual Environment') {
            steps {
                sh 'python3 -m venv /opt/venv'  // Crea un entorno virtual en /opt/venv
                sh '/opt/venv/bin/pip install --upgrade pip'  // Actualiza pip dentro del entorno virtual
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '/opt/venv/bin/pip install -r requirements.txt || /opt/venv/bin/pip install pytest'  // Instala las dependencias dentro del entorno virtual
            }
        }

        stage('Test') {
            steps {
                sh '/opt/venv/bin/pytest --junitxml=report.xml'  // Ejecuta las pruebas dentro del entorno virtual
            }
        }

        stage('Archive Results') {
            steps {
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
