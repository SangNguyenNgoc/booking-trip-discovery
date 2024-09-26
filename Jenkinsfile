pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = 'discovery.yml'
        WORKING_DIRECTORY = '/root/mywork/discovery/booking-trip-discovery'
    }

    stages {
        stage('Change Directory') {
            steps {
                dir("${WORKING_DIRECTORY}") {
                    echo 'Changed to working directory'
                }
            }
        }

        stage('Pull from Git') {
            steps {
                dir("${WORKING_DIRECTORY}") {
                    // Pull code từ nhánh master
                    git branch: 'master', url: 'https://github.com/SangNguyenNgoc/booking-trip-discovery.git'
                }
            }
        }

        stage('Docker Compose') {
            steps {
                dir("${WORKING_DIRECTORY}") {
                    // Chạy Docker Compose với cờ -f
                    sh "docker-compose -f ${DOCKER_COMPOSE_FILE} up -d --build"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
