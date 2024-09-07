pipeline {
    agent any
    environment {
        MAX_SIZE = 100
        MIN_SIZE = 10
    }
    tools {
        maven 'mavin-3.9.5'
    }
    options {
        copyArtifactPermission 'read-artifact'
    }
    parameters {
        string(name: 'ENVIRONMENT',
                 defaultValue: 'DEV',
                 description: 'select deployment enviroment')

        text(name: 'PHRASE',
                 defaultValue: 'It was the best of times, it was the worst of times',
                 description: 'Enter a long phrase of text')

        booleanParam(name: 'RUN_TESTS',
                       defaultValue: 'true',
                       description: 'Toggle this value to run tests.')

        choice(name: 'AWS_REGION',
                 choices: ['us-east-1', 'us-east-2', 'us-west-1', 'us-west-2'],
                 description: 'Select the AWS region for deployment.')

        password(name: 'DATABASE_PASSWORD',
                   defaultValue: '100MY_DATABASE_PASSWORD!',
                   description: 'Enter DB2 database password!')
    }
    options {
        // only keep 5 logs for no more than 10 days
        buildDiscarder(logRotator(daysToKeepStr: '10', numToKeepStr: '5'))

        // cause the build to timeout if it runs for more than an hour
        timeout(time: 1, unit: 'HOURS')

        // add time staps to log files
        timestamps()
    }
    stages {
        stage('Checkout SCM....') {
            steps {
                echo 'Checking out Jenkinsfile from Github....'
                echo  "BUILD_DISPLAY_NAME         =  ${BUILD_DISPLAY_NAME}"
                echo  "WORKSPACE                  =  ${WORKSPACE}"
            }
        }
        stage('Build') {
            steps {
                echo 'Building....'
                echo "the MAX_SIZE = ${env.MAX_SIZE}"
                echo "the MIN_SIZE = ${env.MIN_SIZE}"
                echo  "currentBuild.projectName              =  ${currentBuild.projectName}"
                echo  "currentBuild.id                       =  ${currentBuild.id}"
            }
        }
        stage('source maven'){
            steps {
                sh 'mvn --version'
                sh 'git --version'
            }
        }
        stage('Test....') {
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
        stage('Report and Archive....') {
            steps {
                echo 'Reporting....'
                sh 'echo "this is a text report generated and archived by a Jenkins pipeline" >> 3stage-report.txt'

                echo 'Archiving....'
                archiveArtifacts allowEmptyArchive: true,
                    artifacts: '*.txt',
                    fingerprint: true,
                    followSymlinks: false,
                    onlyIfSuccessful: true
            }
        }
    }
}
