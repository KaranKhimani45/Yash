pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        TOMCAT_URL = 'http://13.60.17.20/:9000'
        TOMCAT_CREDENTIALS = 'tomcat-creds'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/KaranKhimani45/Yash.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: env.TOMCAT_CREDENTIALS,
                        path: '',
                        url: "${env.TOMCAT_URL}"
                    )
                ],
                contextPath: 'sample-app',
                war: 'target/sample-app.war'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
