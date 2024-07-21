pipeline {
    agent any
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') { 
            steps {
                sh 'npm run build' 
            }
        }
        stage('Deliver') {
            steps {
                sh '''
                npm start &
                echo $! > .pidfile
                '''
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh '''
                kill $(cat .pidfile)
                rm .pidfile
                '''
            }
        }
        stage('Test'){
            steps{
                sh "./jenkins/scripts/test.sh"
            }
        }
    }
}
