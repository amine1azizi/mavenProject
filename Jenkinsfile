pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'MAVEN'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Getting code from GitHub...'
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Running Maven tests with MySQL...'
                sh 'mvn clean test'
            }
        }

        stage('Build JAR') {
            steps {
                echo 'Building full project...'
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube...'
                withSonarQubeEnv('sonar') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Archive JAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "BUILD SUCCESS — Everything is green!"
        }
        failure {
            echo "BUILD FAILED"
        }
    }
}
