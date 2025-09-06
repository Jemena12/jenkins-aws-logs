pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
        AWS_DEFAULT_REGION    = 'us-east-1'
        LOG_GROUP             = 'LeancoreInfraStackProd-LeancorePortfolioReporterTaskleancoreportfolioreporterLogGroupD62FBEF1-V5zAjptjzyox'
    }

    stages {
        stage('Instalar dependencias') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Ejecutar script') {
            steps {
                sh './venv/bin/python export_logs.py'
            }
        }

        stage('Guardar artefactos') {
            steps {
                archiveArtifacts artifacts: 'logs_export.csv', fingerprint: true
            }
        }
    }
}
