pipeline {
	agent {
		node {
			label 'master'
		}
	}
	
	options{
		timestamps()
	}
	
	
	stages{
		stage("Checkout, Test & Publish") {
			steps{
				checkout scm
				
				script{
					sh(/mvn clean  test /)
				}
				
				step([$class : 'Publisher', reportFilenamePattern : '**/testng-results.xml'])
			}
		}
		
		stage("Email"){
			steps{
				emailext (to: 'bharath.selenium26@gmail.com', replyTo: 'bharath.selenium26@gmail.com', subject: "Email Report from - '${env.JOB_NAME}' ", body: readFile("target/surefire-reports/emailable-report.html"), mimeType: 'text/html');
			}
		}
	}
	

}
