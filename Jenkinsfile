pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/michellemontoya/ejemplo-python.git', branch: 'main'
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                // Asegúrate de que el entorno virtual ya esté creado
                sh 'source /path/to/existing/venv/bin/activate'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '/path/to/existing/venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh '/path/to/existing/venv/bin/pytest --junitxml=report.xml'
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
