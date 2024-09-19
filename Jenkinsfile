pipeline {
    agent any

    stages {
        
       /* stage('build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            environment {
                // Set NPM cache directory to a writable location
                NPM_CONFIG_CACHE = '/tmp/.npm'
            }
            steps {
                sh '''
                echo "Starting build process..."
                
                echo "Cleaning up workspace..."
                rm -rf node_modules

                echo "Setting up npm cache directory..."
                mkdir -p /tmp/.npm

                echo "Cleaning npm cache..."
                npm cache clean --force

                echo "Checking npm version..."
                npm --version

                echo "Installing dependencies..."
                npm ci --unsafe-perm

                echo "Running build..."
                npm run build --unsafe-perm

                echo "Listing files..."
                ls -la
                '''
            }
        }
        */

        stage ('test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'test -f build/index.html'
                sh 'npm test'
            }
        }
            stage ('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.47.1-noble'
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm install serve
                node_modules/.bin/serve -s build &
                sleep 10
                npx playwright test
                '''
            }

        }
    }
    }


