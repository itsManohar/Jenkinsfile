pipeline {
    agent any
    tools {
        maven 'maven.3.8.1'
        jdk 'jdk8u221'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

        stage ('Build') {
            steps {
                 bat 'mvn -Dmaven.test.failure.ignore=true install' 
                # sh 'mvn -Dmaven.test.failure.ignore=true install' 
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
