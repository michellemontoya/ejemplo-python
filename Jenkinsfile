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
                script {
                    // Crear un entorno virtual
                    sh 'python3 -m venv venv'
                    // Activar el entorno virtual
                    sh 'source venv/bin/activate'
                    // Instalar pip dentro del entorno virtual
                    sh 'python3 -m ensurepip --upgrade'
                    // Instalar las dependencias desde el requirements.txt
                    sh 'pip install -r requirements.txt'
                    // Si no tienes un requirements.txt, usa algo como:
                    // sh 'pip install pytest'
                }
            }
        }

        stage('Test') {
            steps {
                sh 'pytest --junitxml=report.xml'
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
