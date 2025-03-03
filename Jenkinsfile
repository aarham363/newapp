pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git(
                    branch: 'main',
                    url: 'https://github.com/aarham363/newapp.git',
                    credentialsId: 'github-auth'  // Must match Jenkins credentials
                )
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x gradlew'  // Fixed command
                sh './gradlew clean assembleDebug'
            }
        }
        
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
        
        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'app/build/outputs/apk/debug/app-debug.apk'
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}