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
        stage('Test') {
            steps {
                sh """
                echo 'Testing....'
                """
            }
        }
        stage('Example') {
            steps {
                sh """
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"
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
        }
        failure {
            echl "I will run on failuer"
        }
        success{
            echo "I will run on scuuess inly"
        }
    }
}

