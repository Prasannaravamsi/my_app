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
	      options {
                timeout(time: 10, unit: 'SECONDS') 
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
        stage('bug') {
            steps {
                retry(3) {
                    echo 'in the retry loop'
                    //throw new Exception('failing in retry loop') // This runs (when uncommented) several times before the pipeline exits with failure.
                    build(job: 'pipeline', propagate: true) // This only runs once before the pipeline exits with failure.
                }
            }
   
		}
   }
    
}
