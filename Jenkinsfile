pipeline{
    agent any    
    tools{
        nodejs "NodeJS"
    }
    stages{
        stage('Checkout'){
            steps{
                checkout scm
            }
        }
        stage ('Install'){
            steps{
                //similar to npm install but is used in automated enviroments like CI/CD
                sh 'npm ci'
//                sh 'npm i sonar-scanner --save-dev'
            }
        }
        stage("Test"){
            steps{
                sh "npm test"  
            }
       }
//         stage('SonarQube Analysis') {
//            steps{
//                withSonarQubeEnv('aline-sonarqube-server') {
//                    sh "npm run sonar-scanner -Dsonar.projectKey=Admin-Portal-Project"
//                }
//            }
//        }
//        stage('Quality Gate'){
//            steps{
//                waitForQualityGate abortPipeline: true
//            }
//        }
        stage("Build"){
            steps{
                sh "CI=false npm run build"
            }
        }
    }
    post{
        always{
            archiveArtifacts artifacts: 'build/*/*', onlyIfSuccessful: true
        }
    }
}