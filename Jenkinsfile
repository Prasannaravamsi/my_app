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
			stage('Test On Windows') {
				steps {
					echo "Test windows"
				    }   
                    }
			stage('Test on Linux') {
                steps {
					echo "Test Linux"
				    }   
					}
					}
					}
		stage ("Build"){
			steps {
				sh 'mvn -Dmaven.test.failure.ignore=true install'
				}
				}
}
}
