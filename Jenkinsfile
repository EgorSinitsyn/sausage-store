pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *') // Запуск по крону
    }

    tools {
        maven 'maven-3.9.9'
        jdk 'jdk-16'
        nodejs 'node-10'
    }

    stages {
        stage('Build & Test backend') {
            steps {
                dir("backend") {
                    sh 'mvn package'
                }
            }

            post {
                success {
                    junit 'backend/target/surefire-reports/**/*.xml'
                }
            }
        }

        stage('Build frontend') {
            steps {
                dir("frontend") {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Save artifacts') {
            steps {
                archiveArtifacts artifacts: 'backend/target/sausage-store-0.0.1-SNAPSHOT.jar'
                archiveArtifacts artifacts: 'frontend/dist/frontend/*'
            }

            post {
                success {
                    script {
                        // Получаем название ветки и убираем префикс origin/
                        def branchName = env.GIT_BRANCH.replaceFirst(/^origin\//, '')

                        // Данные для отправки уведомления в Telegram
                        def chatId = '453143628'
                        def botToken = '7036490341:AAGwX_b_MUgRy2wJz4q-fdkIxMr4ANU51eQ'
                        def message = "Приложение в ветке ${branchName} успешно собрано !!!"

                        // Выполняем curl для отправки нотификации
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
}
