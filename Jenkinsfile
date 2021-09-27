pipeline {
    agent any
    tools {
        maven 'maven.3.8.2'
        jdk 'jdk8u221'
    }
    stages {
        stage ('Initialize') {
            steps {
                echo "Starting the pipeline"
               //  sh '''
                //    echo "PATH = ${PATH}" || true
                //    echo "M2_HOME = ${M2_HOME}" || true
               // '''
            }
        }

        stage('Check the ENV'){
            def checkOs(){
                    if (isUnix()) {
                        def uname = sh script: 'uname', returnStdout: true
                        if (uname.startsWith("Darwin")) {
                            return "Macos"
                        }
                        // Optionally add 'else if' for other Unix OS  
                        else {
                            return "Linux"
                        }
                    }
                    else {
                        return "Windows"
                    }
                }
        }
        stage ('Build') {
            steps {
                 bat 'mvn -Dmaven.test.failure.ignore=true install' 
                //  sh 'mvn -Dmaven.test.failure.ignore=true install' 
                echo "done"
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
    }
}
