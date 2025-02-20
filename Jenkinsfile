pipeline {
    agent any
    
    triggers {
        cron('H/10 * * * MON') // Run every 10 minutes on Mondays
    }
    
    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
        
        stage('Code Coverage') {
            steps {
                sh './mvnw org.jacoco:jacoco-maven-plugin:prepare-agent install'
                sh './mvnw org.jacoco:jacoco-maven-plugin:report'
                
                jacoco(
                    execPattern: '**/target/jacoco.exec',
                    classPattern: '**/target/classes',
                    sourcePattern: '**/src/main/java'
                )
            }
        }
    }
    
    post {
        success {
            archiveArtifacts artifacts: '**/target/*.jar'
        }
    }
}