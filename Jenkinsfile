pipeline {
    agent {
        node {
            label 'AGENT-1' // Corrected syntax: 'label' instead of '='
        }
    }
    environment {
           packageVersion=''
    }
   
    stages {
        stage('Get the vesrion') {
            steps {
               script{
                def packageJson = readJSON file: 'package.json'
                 packageVersion = packageJson.version
                 echo "application version is ${packageVersion}"

               }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh """
                npm install
                """
            }
        }
        stage('Zip') {
            steps {
                sh """
               ls -la
               zip -q -r catalogue.zip ./* -x "*.git" -x "*.zip"
               ls -la
                """
            }
        }
        stage('Deploy') {
            steps {
                sh """
                   echo 'here is hell'
               
                """
            }
        }
    }
    post {
        always {
            echo 'will run always'
           /*deleteDir() */
        }
        failure {
            echl "I will run on failuer"
        }
        success{
            echo "I will run on scuuess inly"
        }
    }
}

