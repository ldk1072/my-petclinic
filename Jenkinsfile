pipeline {
    agent { label 'linux01' }
    stages {
        stage ('Checkout') {
            agent { docker 'maven:3.5-alpine' }
          steps {
            git 'https://github.com/effectivejenkins/spring-petclinic.git'
          }
        }
        stage('Build') {
            agent { docker 'maven:3.5-alpine' }
            steps {
                sh 'mvn clean package'
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Deploy') {
            steps {
                input 'Do you approve the deployment?'
                echo "deploying..."
            }
        }
    }
}
