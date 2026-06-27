pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Restore') {
            steps {
                bat 'dotnet restore Homies.sln'
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build Homies.sln --no-restore --configuration Release'
            }
        }
        stage('Test') {
            steps {
                bat 'dotnet test Homies.sln --no-build --configuration Release --logger "trx;LogFileName=test-results.trx"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/test-results.trx', allowEmptyArchive: true
        }
    }
}
