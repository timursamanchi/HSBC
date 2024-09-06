pipeline {
    agent any
    environment {
        MAX_SIZE = 100
        MIN_SIZE = 10
    }
    stages {
        stage('Requirements') {
            steps {
                echo 'Getting Requirements....'
            }
        }
        stage('Build') {
            steps {
                echo 'Building....'
                echo "the MAX_SIZE = ${env.MAX_SIZE}"
                echo "the MIN_SIZE = ${env.MIN_SIZE}"
            }
        }
        stage('Test') {
            environment {
                MAX_SIZE = 9999
                MIN_SIZE = 9
            }
            steps {
                echo 'Testing..1'
                echo 'Testing..2'
                echo 'Testing..3'
                echo "the MAX_SIZE = ${env.MAX_SIZE}"
                echo "the MIN_SIZE = ${env.MIN_SIZE}"
            }
        }
        stage('Report') {
            steps {
                echo 'Reporting....'
                sh 'echo "this is a text report generated and archived by a Jenkins pipeline" >> 3stage-report.txt'
                archiveArtifacts allowEmptyArchive: true,
                    artifacts: '*.txt',
                    fingerprint: true,
                    followSymlinks: false,
                    onlyIfSuccessful: true
            }
        }
    }
}