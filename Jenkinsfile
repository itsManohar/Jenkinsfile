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
            def getOs(){
    String osname = System.getProperty('os.name');
    if (osname.startsWith('Windows'))
        return 'windows';
    else if (osname.startsWith('Mac'))
        return 'macosx';
    else if (osname.contains('nux'))
        return 'linux';
    else
        throw new Exception("Unsupported os: ${osname}");
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
