pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven-3.8.2/bin"
    }
    stages{
        stage('GetCode') {
            steps {
                script {
                    // Checkout the code
                    def code = git 'https://github.com/itraveena/sonarjenkins.git'
                    if (code == 0) {
                        echo 'Code checkout successful!'
                    } else {
                        error 'Failed to checkout code!'
                    }
                }
            }
        }
       
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }
        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube-9.9.2') { 
        // If you have configured more than one global server connection, you can specify its name
//      sh "${scannerHome}/bin/sonar-scanner"
        sh "mvn sonar:sonar"
    }
        }
        }
       
    }
}
