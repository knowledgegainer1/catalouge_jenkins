pipeline {
    agent any 
    // {
    //     node {
    //         label 'AGENT-1' // Corrected syntax: 'label' instead of '='
    //     }
    // }
    environment {
           packageVersion=''
           nexusurl='3.82.112.33:8081'
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
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${nexusurl}",
                    groupId: 'com.roboshop',
                    version: "${packageVersion}",
                    repository: 'catalogue',
                    credentialsId: 'nexusid',# give cred in jenkins crdenials
                    artifacts: [
                        [artifactId: catalogue,
                        classifier: '',
                        file: catalogue.zip,
                        type: 'zip']
                        ]
                )
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

