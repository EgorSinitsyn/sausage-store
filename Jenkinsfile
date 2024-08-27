pipeline {
    agent any // Выбираем Jenkins агента, на котором будет происходить сборка: нам нужен любой

    triggers {
        pollSCM('H/5 * * * *') // Запускать будем автоматически по крону примерно раз в 5 минут
    }

    tools {
        maven 'maven-3.9.9' // Для сборки бэкенда нужен Maven
        jdk 'jdk-16' // И Java Developer Kit нужной версии
        nodejs 'node-10' // А NodeJS нужен для фронта
    }

    stages {
        stage('Build & Test backend') {
            steps {
                dir("backend") { // Переходим в папку backend
                    sh 'mvn package' // Собираем мавеном бэкенд
                }
            }

            post {
                success {
                    junit 'backend/target/surefire-reports/**/*.xml' // Передадим результаты тестов в Jenkins
                }
            }
        }

        stage('Build frontend') {
            steps {
                dir("frontend") {
                    sh 'npm install' // Для фронта сначала загрузим все сторонние зависимости
                    sh 'npm run build' // Запустим сборку
                }
            }
        }

        stage('Save artifacts') {
            steps {
                archiveArtifacts artifacts: 'backend/target/sausage-store-0.0.1-SNAPSHOT.jar'
                archiveArtifacts artifacts: 'frontend/dist/frontend/*'

                script {
                    def chatId = '453143628'
                    def botToken = '7036490341:AAGwX_b_MUgRy2wJz4q-fdkIxMr4ANU51eQ'
                    def message = "Приложение успешно собрано."

                    sh """
                        curl -X POST -H 'Content-type: application/json' \
                        --data '{"chat_id": "${chatId}", "text": "${message}"}' \
                        https://api.telegram.org/bot${botToken}/sendMessage
                    """
                }
            }
        }
    }
}
