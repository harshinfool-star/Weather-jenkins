pipeline {
    agent any
    
    environment {
        // Define project-specific variables
        PROJECT_NAME = 'weather-dashboard'
        BUILD_ID = "${env.BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo '📥 Checking out code from repository...'
                // Git checkout happens automatically in Jenkins
                echo "Building project: ${PROJECT_NAME}"
            }
        }
        
        stage('Validate HTML') {
            steps {
                echo '✅ Validating HTML files...'
                script {
                    // Check if index.html exists
                    if (fileExists('index.html')) {
                        echo '✓ index.html found'
                    } else {
                        error '✗ index.html not found!'
                    }
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                echo '🧪 Running tests...'
                script {
                    // Simple validation tests
                    def htmlContent = readFile('index.html')
                    
                    if (htmlContent.contains('Live Dashboard')) {
                        echo '✓ Page title found'
                    } else {
                        error '✗ Page title not found'
                    }
                    
                    if (htmlContent.contains('getWeather')) {
                        echo '✓ Weather function found'
                    } else {
                        error '✗ Weather function not found'
                    }
                    
                    echo '✓ All tests passed!'
                }
            }
        }
        
        stage('Build') {
            steps {
                echo '🔨 Building the application...'
                script {
                    // Create a build directory
                    sh 'mkdir -p build'
                    
                    // Copy HTML file to build directory
                    sh 'cp index.html build/'
                    
                    echo "✓ Build ${BUILD_ID} completed successfully"
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo '🚀 Deploying to staging environment...'
                script {
                    // Simulate deployment
                    sh 'mkdir -p staging'
                    sh 'cp build/index.html staging/'
                    
                    echo '✓ Deployed to staging successfully'
                    echo "Access your app at: file://${WORKSPACE}/staging/index.html"
                }
            }
        }
        
        stage('Approval') {
            steps {
                echo '⏸️  Waiting for manual approval to deploy to production...'
                // In a real scenario, you might want manual approval
                // Commented out for automatic execution
                // input message: 'Deploy to Production?', ok: 'Deploy'
                echo '✓ Approval received (auto-approved for demo)'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo '🚀 Deploying to production environment...'
                script {
                    // Simulate production deployment
                    sh 'mkdir -p production'
                    sh 'cp build/index.html production/'
                    
                    echo '✓ Deployed to production successfully!'
                    echo "Production URL: file://${WORKSPACE}/production/index.html"
                }
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline completed successfully!'
            echo "Build #${BUILD_ID} of ${PROJECT_NAME} is ready"
            echo "═══════════════════════════════════════"
            echo "Deployment Summary:"
            echo "  Staging: ${WORKSPACE}/staging/index.html"
            echo "  Production: ${WORKSPACE}/production/index.html"
            echo "═══════════════════════════════════════"
        }
        
        failure {
            echo '❌ Pipeline failed!'
            echo 'Please check the logs above for errors'
        }
        
        always {
            echo '🧹 Cleaning up...'
            // Archive artifacts
            archiveArtifacts artifacts: 'build/**/*', fingerprint: true, allowEmptyArchive: true
        }
    }
}
