pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    git credentialsId: 'github-credentials-id', url: 'https://github.com/JDario-Hernandez/Integraci-n-continua-backend-GR-12-B01.git'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build('tienda-perros', '.')
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('tienda-perros').inside {
                        sh 'mvn test'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'docker run -d --name tienda-perros -p 8082:80 tienda-perros'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'El pipeline se ejecutó correctamente.'
        }
        failure {
            echo 'El pipeline falló.'
        }
    }
}
