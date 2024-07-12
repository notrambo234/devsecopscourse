pipeline {
  agent any
  tools { 
        maven 'maven_3_2_5'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=notrambo234webapp -Dsonar.organization=notrambo234 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=897a2a92da4c57faa484e2f879b3716be2036e6c'
			}
        } 
  }
}
