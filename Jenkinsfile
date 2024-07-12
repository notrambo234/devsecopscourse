pipeline {
    agent any
    tools { 
         maven 'maven_3_2_5'  
    }
    stage('checkout') {
        steps {
            git 'https://github.com/notrambo234/devsecopscourse'
        }
    }
    stage('Build') {
        steps {
            sh 'mvn install'
        }
    }
    stage('Test'){
        steps {
            sh 'mvn test'
        }
    }
    stage('SAST Scan') {
        steps {
            sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=notrambo234webapp -Dsonarorganization=notrambo234webapp -Dsonar.host.url=https://sonarcloud.io -Dsobar.token=897a2a92da4c57faa484e2f879b3716be2036e6c'
        }
    }
}