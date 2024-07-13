pipeline {
  agent any
  tools { 
        maven 'maven_3_2_5'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=test123key -Dsonar.organization=test123key -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=897a2a92da4c57faa484e2f879b3716be2036e6c'
			}
        } 
  

    stage('RunSCAAnalysisUsingSnyk') {
            steps {
                                    withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                                         sh 'mvn snyk:test -fn'
                                         }
                                    }
    }
 }
}