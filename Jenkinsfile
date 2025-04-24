pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { git 'https://github.com/michellemontoya/ejemplo-python.git' }
        }
        stage('Test') {
            steps {
                sh 'pip install pytest'
                sh 'pytest'
            }
        }
    }
}
