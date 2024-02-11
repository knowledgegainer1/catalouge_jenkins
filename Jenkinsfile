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
        stage('Install dependencies') {
            steps {
              sh """
              npm install
              """
            }
        }

        stage('Build') {
            steps {
                sh """
                  ls -la
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
