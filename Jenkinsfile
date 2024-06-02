pipeline {
    agent any

    environment {
        APP_NAME = 'my-typescript-app'
        BUILD_IMAGE = "${APP_NAME}-build"
        TEST_IMAGE = "${APP_NAME}-test"
        DEPLOY_IMAGE = "${APP_NAME}"
        //REGISTRY_URL = 'your-docker-registry-url'
        //REGISTRY_CREDENTIALS = 'docker-registry-credentials-id'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Dawid511/webpack-typescript-jest-less'
            }
        }

        stage('Build') {
            steps {
                script {
                    docker.build("${BUILD_IMAGE}", '-f ./build/Dockerfile .')
                }
            }
        }

        stage('Test') {
            steps {
                script {
                   docker.build("${TEST_IMAGE}", '-f ./test/Dockerfile .')
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    docker.build("${DEPLOY_IMAGE}", '.')
                }
            }
        }


        stage('Deploy') {
            steps {
                script {
                    sh '''
                    docker run -d -p 8080:8080 --name ${APP_NAME} ${DEPLOY_IMAGE}
                    '''
                }
            }
        }
    }

    post {
        always {
            script {
                sh '''
                docker rmi ${BUILD_IMAGE} || true
                docker rmi ${DEPLOY_IMAGE} || true
                '''
            }
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
