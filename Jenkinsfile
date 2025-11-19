pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code GitHub...'
                checkout scm
            }
        }

        stage('Build sans tests') {
            steps {
                echo 'Compilation et packaging avec Maven...'
                sh 'mvn -B clean install -DskipTests'
            }
        }

        stage('Archive JAR') {
            steps {
                echo 'Archivage du JAR...'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true, onlyIfSuccessful: true
            }
        }
    }

    post {
        success {
            echo '====================================='
            echo '   BUILD VERT EN MOINS DE 20 SECONDES !'
            echo '   Bravo Mahdi, ton CI est parfait !'
            echo '====================================='
        }
        failure {
            echo 'Build échoué – regarde les logs ci-dessus'
        }
    }
}
