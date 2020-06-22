pipeline {
   agent any
   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
         }
      }
      stage ('Input directive '){
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
                            stage('Unit Test') {
                           steps {
                                echo "Running the unit test..."
                           }
                           }
                            stage('Integration test') {
                              agent any
                                    docker {
                                            reuseNode true
                                            image 'ubuntu'
                                           }
                                    
                              steps {
                                echo "Running the integration test..."
                              }
			    }
		   }
	   }
			   
   }
}
