 pipeline{
 
        agent {
                docker {
                image 'maven'
                args '-v $HOME/.m2:/root/.m2
				}
			}

		   stages{
		   
				stage('Quality gate check status')
					 steps{
						script{
					 withSonarQubeEnv('sonarqubeserver')
					 sh "mvn sonar:sonar"
					 
					 timeout(time: 1,unit: 'HOURS') {
				     def qg = waitForQualityGate()
					     if (qg.status ! ='OK') {
						  error "pipeline aborted: $(qg.status)"
						  }
						  
						sh "mvn clean install"

						}
					 }
                   }
				   
				}
	}			
