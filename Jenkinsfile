pipeline {
    agent any

    tools {
        // Якщо в Jenkins налаштовані JDK та Maven - вкажи їх імена
        jdk 'AdoptOpenJDK-17'
        maven 'Maven-3.9.6'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/raccoontop/practica7.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh './mvnw clean compile'
            }
        }
        stage('Test') {
            steps {
                sh './mvnw test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            steps {
                sh './mvnw package -DskipTests'
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}