pipeline {
    agent any
    
    triggers {
		cron('H/10 * * * 1') // Run every 10 minutes on Monday
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