pipeline {
agent any
  tools { 
       maven 'maven' 
        jdk 'JAVA_HOME'  
    }
stages {
stage ("compile stage"){
steps{
bat 'mvn clean compile'
}
}
}
}
