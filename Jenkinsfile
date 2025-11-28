pipeline {
    agent any

    environment {
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

        stage('Backend – npm install & test') {
            when {
                expression { 
                    fileExists("${env.BACKEND_DIR}") && 
                    fileExists("${env.BACKEND_DIR}/package.json")
                }
            }
            steps {
                echo "📦 Backend detected at ${env.BACKEND_DIR} (package.json present)"
                dir(env.BACKEND_DIR) {
                    sh 'npm install'
                    // if you have tests:
                    // sh "npm test"
                }
            }
        }

        stage('Frontend – npm install & build') {
            when {
                expression { 
                    fileExists("${env.FRONTEND_DIR}") && 
                    fileExists("${env.FRONTEND_DIR}/package.json")
                }
            }
            steps {
                echo "🎨 Frontend detected at ${env.FRONTEND_DIR} (package.json present)"
                dir(env.FRONTEND_DIR) {
                    sh 'npm install'
                    // React/Vite/etc:
                    sh 'npm run build'
                }
            }
        }

        stage('Docker – build & compose up') {
            when {
                expression { fileExists('docker-compose.yml') }
            }
            steps {
                echo "🐳 docker-compose.yml found – running docker compose"
                // These will work if Jenkins container has docker CLI + /var/run/docker.sock mounted
                sh 'docker compose down || true'
                sh 'docker compose up -d --build'
            }
        }
    }

    post {
        always {
            echo "🏁 EMS pipeline finished (success or failure)"
        }
        success {
            echo "🎉 EMS build & (optional) docker deploy succeeded"
        }
        failure {
            echo "❌ EMS pipeline failed – check the stage that broke above"
        }
    }
}
