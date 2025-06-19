pipeline {
    agent any

    environment {
        NODE_ENV = 'test'
    }

    tools {
        nodejs 'NodeJS' // Това име трябва да съвпада с NodeJS tool, конфигуриран в Jenkins (Manage Jenkins > Global Tool Configuration)
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mihaylov79/02StudentRegistryApp.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Start App (Background)') {
            steps {
                // Стартиране на приложението във фонов режим
                sh 'nohup npm start &'
                // Изчакване приложението да стартира (примерно 5 сек)
                sh 'sleep 5'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build and test succeeded.'
        }
        failure {
            echo 'Build or test failed.'
        }
    }
}
