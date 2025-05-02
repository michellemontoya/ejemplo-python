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

        stage('Ejecutar pruebas y generar reporte') {
            steps {
                sh '''
                    if [ -d tests ]; then
                        mkdir -p reports
                        python3 -m xmlrunner discover -s tests -o reports || echo "Fallo la ejecución de pruebas"
                    else
                        echo "No hay carpeta de tests"
                    fi
                '''
            }
        }

        stage('Publicar reporte') {
            steps {
                junit 'reports/**/*.xml'
            }
        }
    }
}