pipeline {
    agent any
    
	environment {
        JAVA_HOME = "${env.JAVA_HOME}"
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }
	
    triggers {
        cron('H/10 * * * 1')
    }
    
    stages {
        stage('Build') {
            steps {
                bat './mvnw clean package'
            }
        }
        
        stage('Code Coverage') {
            steps {
                bat './mvnw org.jacoco:jacoco-maven-plugin:prepare-agent install'
                bat './mvnw org.jacoco:jacoco-maven-plugin:report'
                
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