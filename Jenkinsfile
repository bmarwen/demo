pipeline {
    agent any // This uses any available agent or node

    environment {
        SONARQUBE = 'MySonarQube' // Name of the SonarQube server configuration in Jenkins
        SONARQUBE_SCANNER = tool name: 'SonarQube Scanner', type: 'SonarQubeScannerInstallation'
    }

    stages {
        stage('Build') {
    steps {
        parallel(
            composer: {
                sh 'composer install --prefer-dist --optimize-autoloader'
                sh 'composer require --dev phpmetrics/phpmetrics friendsofphp/php-cs-fixer --no-interaction --prefer-dist --optimize-autoloader'
            },
            'prepare-dir': {
                sh 'rm -Rf ./build/'
                sh 'mkdir -p ./build/coverage'
                sh 'mkdir -p ./build/logs'
                sh 'mkdir -p ./build/phpmetrics'
            }
        )
    }
}
    }

    post {
       
    }
}
