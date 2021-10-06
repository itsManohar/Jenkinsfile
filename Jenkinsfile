pipeline {
    agent any
    tools {
        maven 'maven.3.8.2'
        jdk 'jdk8u221'
    }
    stages {
        stage ('Initialize STAGE') {
        
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
        
            stage('Stage A') {
            steps {
                script {
                    // tee log into file
                    tee(STAGE_A_LOG_FILE) {
                        echo 'print some Stage_A log content ...'
                    }
                }
            }
        }
        stage('Stage B') {
            steps {
                script {
                    // search log file for 'Stage_A'
                    regex = java.util.regex.Pattern.compile('some (Stage_A) log')
                    matcher = regex.matcher(readFile(STAGE_A_LOG_FILE))
                    if (matcher.find()) {
                        echo "found: ${matcher.group(1)}"
                    }
                }
            }
        }
        
        
        stage ('Building STAGE') {
            
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
