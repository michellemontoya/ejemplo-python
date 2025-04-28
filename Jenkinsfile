pipeline {
    agent { label 'agent1' }

    stages {
        stage('Descargar código') {
            steps {
                git branch: 'main', url: 'https://github.com/michellemontoya/ejemplo-python.git'

            }
        }

        stage('Instalar dependencias') {
            steps {
                sh '''
                    if [ -f requirements.txt ]; then
                        pip install -r requirements.txt || echo "Fallo la instalación de dependencias"
                    else
                        echo "No hay requirements.txt"
                    fi
                '''
            }
        }

        stage('Ejecutar pruebas') {
            steps {
                sh '''
                    if [ -d tests ]; then
                        python3 -m unittest discover tests || echo "Fallo la ejecución de pruebas"
                    else
                        echo "No hay carpeta de tests"
                    fi
                '''
            }
        }
    }
}

