pipeline {
    agent { label 'agent1' }

    stages {
        stage('Instalar herramientas necesarias') {
            steps {
                sh '''
                    echo "Actualizando paquetes..."
                    apt-get update || true
                    apt-get install -y git python3-pip || true
                '''
            }
        }

        stage('Descargar código') {
            steps {
                git url: 'https://github.com/michellemontoya/ejemplo-python.git', branch: 'main'
            }
        }

        stage('Instalar dependencias') {
            steps {
                sh '''
                    if [ -f "requirements.txt" ]; then
                        pip3 install -r requirements.txt
                    else
                        echo "No se encontró requirements.txt, continuando..."
                    fi
                '''
            }
        }

        stage('Ejecutar pruebas') {
            steps {
                sh '''
                    if [ -d "tests" ]; then
                        python3 -m unittest discover tests
                    else
                        echo "No hay carpeta de tests, saltando pruebas..."
                    fi
                '''
            }
        }
    }

    post {
        always {
            echo '✅ Proceso completado'
        }
        failure {
            echo '❌ Falló el pipeline'
        }
    }
}
