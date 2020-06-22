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
                echo 'Job building'
            }
      }
	   stage ('parallel') {
		   parallel {
			   stage('In Parallel 1') {
			   steps {
                                echo "In Parallel 1"
                            }
			   }
			   stage('In Parallel 2') {
                            steps {
                                echo "In Parallel 2"
                            }
                        }
		   }
	   }
			   
   }
}
