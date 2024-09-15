pipeline {
    agent any

    stages {
        stage('build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh '''
               echo "Cleaning up node_modules..."
               rm -rf node_modules
               echo "Cleaning npm cache..."
               npm cache clean --force
               echo "Installing dependencies..."
               npm ci
               echo "Running build..."
               npm run build
               ls -la
               '''
            }
        }
    }
}
