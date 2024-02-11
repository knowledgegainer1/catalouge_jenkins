pipeline {
    agent {
        node {
            label 'AGENT-1' // Corrected syntax: 'label' instead of '='
        }
    }
    environment {
        packageVersion = ''
    }

    stages {
        stage('Get the version') {
            steps {
                script {
                    def packageJson = readJSON file:'package.json'
                    packageVersion = packageJson.version
                    echo "version is $packageVersion"
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing....'
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
            echo 'will run'
        }
    }
}
