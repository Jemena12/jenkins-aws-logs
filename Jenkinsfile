pipeline {
    agent any

    environment {
        // 🔑 Variables cargadas desde Jenkins Credentials
        AWS_ACCESS_KEY_ID     = credentials('b2a54366-46b0-401e-b460-4b114fb10e92')
        AWS_SECRET_ACCESS_KEY = credentials('954fd517-a973-4ce0-a57d-26bf67465cd8')
        AWS_DEFAULT_REGION    = 'us-east-1'
        LOG_GROUP_NAME        = 'LeancoreInfraStackProd-LeancorePortfolioReporterTaskleancoreportfolioreporterLogGroupD62FBEF1-V5zAjptjzyox'   // cambia según tu caso
    }

    //triggers {
        // Ejecuta cada 5 minutos
       // cron('H/5 * * * *')
  //  }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Jemena12/jenkins-aws-logs.git'
            }
        }

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
