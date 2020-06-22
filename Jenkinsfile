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
                            stage('Master branch') {
                           git url:'https://github.com/Prasannaravamsi/my_app',branch:'master'
                           }
                            stage('feature branch') {
                            git url:'https://github.com/Prasannaravamsi/my_app',branch:'feature'
			    }
		   }
	   }
			   
   }
}
