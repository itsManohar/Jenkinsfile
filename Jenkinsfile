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
        

//         stage('Check the ENV'){
//             steps {
//             def getOs(){
//                     String osname = System.getProperty('os.name');
//                     if (osname.startsWith('Windows'))
//                         return 'windows';
//                     else if (osname.startsWith('Mac'))
//                         return 'macosx';
//                     else if (osname.contains('nux'))
//                         return 'linux';
//                     else
//                         throw new Exception("Unsupported os: ${osname}");
//                 }
//             }
//         }
        
        stage('current OS'){
            steps {
                sh 'echo "currente OS is = " '
                
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
        
        }
        
        stage ('Build') {
            
            when {
         expression { BRANCH_NAME != 'master' }
                }
            steps {
                // bat 'mvn -Dmaven.test.failure.ignore=true install' 
                sh ''' 
                echo "pwd is= ${PWD}"
                
                mvn -Dmaven.test.failure.ignore=true install
                echo "~~~~~~~~~~~~~~~~ done ~~~~~~~~~~~~~~~~"
                sh 'find . -name *.jar' || true
                '''
            }
            
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
    }
}
