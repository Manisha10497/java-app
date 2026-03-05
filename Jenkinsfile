pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    environment {
        SONAR_HOME = tool 'SonarScanner'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Manisha10497/java-app.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t java-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8081:8080 java-app'
            }
        }
    }
}
