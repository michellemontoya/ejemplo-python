pipeline {
    agent { label 'agent1' }

    stages {
        stage('Descargar código') {
            steps {
                git 'https://github.com/michellemontoya/ejemplo-python.git'
            }
        }

        stage('Ejecutar pruebas') {
            steps {
                sh 'pip install -r requirements.txt || echo "No se encontraron dependencias para instalar"'
                sh 'python3 -m unittest discover tests'
            }
        }
    }
}