pipeline {
    agent any
    
    environment {
        SONARQUBE = 'MySonarQube' // Name of the SonarQube server configuration in Jenkins
        SONARQUBE_SCANNER = tool name: 'SonarQube Scanner', type: 'SonarQubeScannerInstallation'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'composer install'
            }
        }
        
        stage('Build') {
            steps {
                sh 'composer build' // Adjust this command based on your build process
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool name: 'SonarQube Scanner', type: 'SonarQubeScannerInstallation'
                    withSonarQubeEnv(SONARQUBE) {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=my-symfony-project -Dsonar.sources=src -Dsonar.host.url=http://localhost:9000 -Dsonar.login=YOUR_SONARQUBE_TOKEN"
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                sh 'php bin/phpunit'
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
