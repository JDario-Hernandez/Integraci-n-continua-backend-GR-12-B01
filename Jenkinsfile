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
                    bat 'docker stop tienda-perros || true'
                    bat 'docker rm tienda-perros || true'
                    bat 'docker rmi tienda-perros || true'
                    docker.build('tienda-perros', '.')
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    bat 'docker run -d --name tienda-perros -p 8081:8081 tienda-perros'
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
