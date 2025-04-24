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
                sh 'pip install -r requirements.txt'
                // Si no tienes un requirements.txt, puedes usar:
                // sh 'pip install pytest'
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
