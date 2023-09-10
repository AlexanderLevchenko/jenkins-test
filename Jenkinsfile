pipeline {
    agent any

    stages {
        stage('Clean Workspace'){
            cleanWs()
          }

          stage("Main build") {
            docker.image('node:10').pull()
            docker.image('ismail0352/chrome-node').pull()

            // Performing Install and Lint
            docker.image('node:10').inside {
              stage('Install') {
                sh label:
                  'Running npm install',
                script: '''
                  node --version
                  cd jenkins-test
                  npm install
                '''
              }

              stage('Lint') {
                sh label:
                  'Running npm run lint',
                script: '''
                  cd jenkins-test
                  npm run lint
                '''
              }
            }

            docker.image('ismail0352/chrome-node').inside('--name chrome-node --security-opt seccomp=$WORKSPACE/chrome.json') {
              stage('Test') {
                sh label:
                  'Running npm run test',
                script: '''
                  node --version
                  cd jenkins-test
                  npm run test
                '''
              }
            }
            stage ('Build') {
              docker.image('node:10').inside {
                sh label:
                  'Running npm run build',
                script: '''
                  node --version
                  cd jenkins-test
                  npm run build
                '''
              }
            }
          }
    }
}
