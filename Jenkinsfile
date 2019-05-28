pipeline {
    agent { 
        docker { 
            image 'node:latest' 
            args '-p 3000:3000' 
        } 
    }
    
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }
    
    stages {

        stage('nodejs stage1') {
            steps {
            // def name = 'yuichi.nagakura'
            // def age = 999
                sh 'npm --version'
                echo "${DB_ENGINE}"
            }
        }
        stage('nodejs stage2') {
            steps {
                echo 'Hello Nodejs'
                echo "${DISABLE_AUTH}"
            }
            post {
                always {
                    echo 'Finished nodejs stage2!'
                }
            }
        }
        stage('nodjs stage3') {
            environment {
                ABC = 'DEF'
            }
    
            steps {
                sh 'echo "Hello ${ABC}"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah > testfile
                '''                
            }
        }
    }
    
    post {
        always {
            echo 'This will always run'
            archiveArtifacts artifacts: 'testfile', fingerprint: true /* store aritifacts */
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}

