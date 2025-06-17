pipeline {
    agent any

    tools {
        jdk 'JDK17'
        sonarQubeScanner 'SonarScanner'
    }

    environment {
        SONARQUBE_TOKEN = credentials('sonarqube-token')
    }

    stages {
        stage('Clone') {
            steps {
                echo "Code cloned automatically by Jenkins."
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonar') {
                    sh 'sonar-scanner -Dsonar.login=$SONARQUBE_TOKEN'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
