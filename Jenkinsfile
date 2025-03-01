pipeline {
    agent any
    
    environment {
        ANDROID_HOME = '/opt/android-sdk'
        GRADLE_USER_HOME = "${WORKSPACE}/.gradle"
    }

    stages {
        stage('Checkout') {
            steps {
                git(
                    branch: 'main',
                    url: 'https://github.com/aarham363/newapp.git',
                    credentialsId: 'github-auth'
                )
            }
        }

        stage('Build') {
            steps {
                sh './gradlew clean assembleDebug'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Lint Check') {
            steps {
                sh './gradlew lintDebug'
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'app/build/outputs/apk/debug/app-debug.apk', fingerprint: true
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}  // ← THIS CLOSING BRACE WAS MISSING