pipeline {
    agent any

    stages {
        stage('npm install') {
            steps {
               echo 'npm install...'
               npm i
           }
        }

        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('lint') {
            steps {
                echo 'Linting...'
            }
        }
    }
}
