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
 
    stage ('Build') {
      steps {
            withDockerRegistry([credentialsId: "dockerlogin", url:""]) {
                  script{
                  app = docker.build("mcm")
                  }
            }
      }
    }
    
    stage ('Push') {
      steps {
            script {
                  docker.withRegistry('https://654654493373.dkr.ecr.us-west-2.amazonaws.com','ecr:us-west-2:aws-credentials'){
                  app.push("latest")
                  }
            }
      }
    }
    stage('Kubernetes Deployment of mcm Buggy Web Application') {
	steps {
	      withKubeConfig([credentialsId: 'kubelogin']) {
		  sh('kubectl delete all --all -n devsecops')
		  sh ('kubectl apply -f deployment.yaml --namespace=devsecops')
		}
	      }
   	}
}
}