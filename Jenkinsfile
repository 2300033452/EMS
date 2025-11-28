pipeline {
    agent any

    environment {
        // change these if your folder names are different
        BACKEND_DIR  = "backend"
        FRONTEND_DIR = "frontend"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Show workspace') {
            steps {
                echo "✅ EMS pipeline is connected and running"
                echo "Workspace: ${pwd()}"
                sh 'ls -R'
            }
        }

        stage('Backend – build/test (placeholder)') {
            when {
                expression { fileExists("${env.BACKEND_DIR}") }
            }
            steps {
                echo "📦 Backend folder found at: ${env.BACKEND_DIR}"
                echo "👉 Here you will run backend build commands."

                // EXAMPLES (pick the one that matches your tech stack later):
                // Node/Express:
                // sh "cd ${env.BACKEND_DIR} && npm install && npm test"

                // Java + Maven:
                // sh "cd ${env.BACKEND_DIR} && mvn clean package"

                // Python:
                // sh "cd ${env.BACKEND_DIR} && pip install -r requirements.txt && pytest"

                sh "cd ${env.BACKEND_DIR} && ls"   // harmless, just to prove it runs
            }
        }

        stage('Frontend – build (placeholder)') {
            when {
                expression { fileExists("${env.FRONTEND_DIR}") }
            }
            steps {
                echo "🎨 Frontend folder found at: ${env.FRONTEND_DIR}"
                echo "👉 Here you will run frontend build commands."

                // For React / Vite / etc. later you can do:
                // sh "cd ${env.FRONTEND_DIR} && npm install && npm run build"

                sh "cd ${env.FRONTEND_DIR} && ls"  // harmless for now
            }
        }
    }

    post {
        always {
            echo "🏁 Pipeline finished (success or failure)"
        }
        success {
            echo "🎉 EMS pipeline finished successfully"
        }
        failure {
            echo "❌ EMS pipeline failed – check logs"
        }
    }
}
