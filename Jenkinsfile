pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-credentials-id', url: 'https://github.com/JDario-Hernandez/Integraci-n-continua-backend-GR-12-B01.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    docker stop tienda-perros || true
                    docker rm tienda-perros || true
                    docker rmi tienda-perros || true
                    docker build -t tienda-perros .
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d --name tienda-perros -p 8081:8081 tienda-perros'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'El pipeline se ejecutó correctamente con push.'
        }
        failure {
            echo 'El pipeline falló.'
        }
    }
}
