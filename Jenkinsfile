pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clonamos el repositorio
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
                sh './venv/bin/python -m unittest test_calculator.py'
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
                // Archivar el archivo de resultados de las pruebas
                archiveArtifacts artifacts: 'report.xml', allowEmptyArchive: true
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
