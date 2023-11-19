pipeline {
    agent {
        docker { 
            image 'epf'
            args '-u root'
        }
    }
    stages {
        stage('Test') {
            steps {
                sh '/usr/local/bin/defaults write Eggplant DisableEACPolling YES'
                sh 'runscript -CommandLineOutput yes -LicenseKey $EPF_LICENSE_KEY'
                sh 'rm -rf GherkinTest.suite/Results'
                sh 'runscript -CommandLineOutput yes GherkinTest.suite/Features/MyFeature.feature'
            }
        }
    }
    post {
        always {
            junit 'GherkinTest.suite/Results/MyFeature-Feature/**/*.xml'
            archiveArtifacts artifacts: 'GherkinTest.suite/Results/MyFeature-Feature/', fingerprint: true
        }
    }
}