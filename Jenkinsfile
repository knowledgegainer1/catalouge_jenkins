pipeline {
    agent {
        node {
            label 'AGENT-1' // Corrected syntax: 'label' instead of '='
        }
    }
    environment {
        packageVersion = ''
        nexusURL='172.31.82.56:8081'
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
                sh '''
              npm install
              '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                  ls -la
                  zip -q -r catalouge.zip ./* -x ".zip" -x "*.git"
                  ls -lrt
                '''
            }
        }
        stage('Publish-Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "$nexusURL",
                    groupId: 'com.roboshop',
                    version: "$packageVersion",
                    repository: 'catalouge',
                    credentialsId: 'Nexus-Auth',
                    artifacts: [
                        [artifactId: 'catalouge',
                        classifier: '',
                        file: 'catalouge-' + version + '.jar',
                        type: 'jar']
                    ]
                )
            }
        }
    }
    post {
        always {
            echo 'will run always'
            deleteDir()
        }
    }
}
