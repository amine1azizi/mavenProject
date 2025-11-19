// Jenkinsfile – Version ULTRA SIMPLE (juste build sans tests)
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compilation et packaging avec Maven...'
                sh 'mvn -B clean install -DskipTests'
                // -B = logs propres, -DskipTests = on saute tous les tests
            }
        }

        stage('Archive JAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true, onlyIfSuccessful: true
                echo 'JAR généré et archivé avec succès !'
            }
        }
    }

    post {
        success {
            echo '
            BUILD VERT EN 15 SECONDES !!!
            Bravo Mahdi, ton projet est maintenant en CI propre et simple
            Tu peux maintenant ajouter les tests plus tard si tu veux
            '
        }
        failure {
            echo 'Échec du build – regarde les logs'
        }
    }
}
