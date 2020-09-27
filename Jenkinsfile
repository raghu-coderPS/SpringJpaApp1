pipeline {

  agent any

  stages {	


	stage('Maven Compile'){

		steps{

			echo 'Project compile stage'

			bat label: 'Compilation running', script: '''mvn compile'''

	       	}

	}

	stage('Unit Test') {

	   steps {

			echo 'Project Testing stage'

			bat label: 'Test running', script: '''mvn test'''

	       

       		}

   	}

	  
	stage('Jacoco Coverage Report') {

        steps{

            jacoco()

		}

	}

	  

	stage('SonarQube'){

         steps{

            bat label: '', script: '''mvn sonar:sonar \

		 -Dsonar.host.url=http://localhost:9000 \

 		-Dsonar.login=ff5c276939ab066fea300810e7006165c6243c7b'''

          }

      }

	  

	stage('Maven Package'){

		steps{

			echo 'Project packaging stage'

			bat label: 'Project packaging', script: '''mvn package'''

		}

	} 		

    

  }
	post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }

}
