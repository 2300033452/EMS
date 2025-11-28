pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Get code from Git
                checkout scm
            }
        }

        stage('Show workspace') {
            steps {
                echo "✅ EMS pipeline is connected and running"
                echo "Workspace: ${pwd()}"
                // List files just to see everything is there
                sh 'ls -R'
            }
        }
    }

    post {
        always {
            echo "🏁 Pipeline finished (success or failure)"
        }
        success {
            echo "🎉 Build finished successfully"
        }
        failure {
            echo "❌ Build failed – check above logs"
        }
    }
}
