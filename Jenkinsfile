pipeline{
	agent any
		stages{
			stage('first'){
				steps{
					echo "Pipeline triggered ..."					
				}	
			}
			
			stage('clean'){
				steps{
					bat "mv clean" 
				}
			}
			
			stage('compile'){
				steps{
					bat "mvn compile"
				}
			}
			stage('sonarqube code check'){
				steps{
					bat "mvn sonar:sonar"
				}
			}
			
			stage('package'){
				steps{
					bat "mvn package"
				}
			}
			
			/*stage('deploy'){
				steps{
					bat "mvn deploy -DmuleDeploy"
				}
			}*/
		}
		
		post {
        	always{
        		echo "pipeline job finished executing ..."	
        	}
        	success{
        		echo "entered success in post action"
				emailext body: 'Jenkins build has executed successfully and the application has been deployed to CloudHub', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Jenkins build success test-repo-one'
			}
			failure{
				echo "entered failure in post action"
				emailext body: 'Jenkins build has failed and the application has not been deployed to Cloudhub', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Jenkins build failed test-repo-one'
			}
    }
				
}