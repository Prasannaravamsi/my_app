pipeline {
   agent any
   tools { 
       maven 'maven' 
        jdk 'JAVA_HOME'  
    }
   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
			}
			}
      stage ('Input directive '){
	      retry(2) {
		      try{
			      timeout(time: 10, unit: 'SECONDS') } catch (err){
			      script{
                  def user = err.getCauses()[0].getUser()
                  error "[${user}] catched timeout! $err"
                }
		      }
	      }
		      input{
            message "Press Ok to continue"
            submitter "user1,user2"
            parameters {
            string(name:'username', defaultValue: 'user', description: 'Username of the user pressing Ok')
            }
		      }
        steps { 
			echo "User: ${username} said Ok."
			}
	      }			
	   stage ('Condition'){
           when {
		   not {
				branch 'master'
			}
            }
            steps {
                echo 'Branch is master'
            }
			}
	   stage ('parallel') {
			parallel {
			stage('Build') {
				steps {
				bat 'mvn clean package'
				    }   
                    }
			stage('Test') {
                	steps {
				bat 'mvn test'	
				    }   
					}
					}
					}
		stage ("Deploy"){
			steps {
		   bat 'java -jar target/my-app-1.0-SNAPSHOT.jar'
			}
    			}
}
}
