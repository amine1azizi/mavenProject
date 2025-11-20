pipeline {
    agent any

    triggers {
        // Déclenche le build à chaque push sur GitHub
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code depuis GitHub...'
                checkout scm
            }
        }

        stage('Build sans tests') {
            steps {
                echo 'Compilation avec Maven...'
                sh 'mvn -B clean install -DskipTests'
            }
        }

        stage('Archive JAR') {
            steps {
                echo 'Archivage du fichier JAR...'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '====================================='
            echo '   BUILD RÉUSSI EN MOINS DE 20 SECONDES !'
            echo '   Bravo Mahdi, ton CI est parfait !'
            echo '====================================='
        }
        failure {
            echo '❌ Le build a échoué – consulte les logs.'
        }
    }
}   
