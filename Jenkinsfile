pipeline {
  agent any
  tools { 
        maven 'maven_3_2_5'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=notrambo234webapp -Dsonar.organization=notrambo234 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=ec7d419cbca51622d92f9c14accf45e5d9da43c0'
			}
        } 
  }
}
