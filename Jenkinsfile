pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run MATLAB Script') {
            steps {
                echo 'Running air_spring_script.m'
                // Use 'bat' if Jenkins is on Windows, 'sh' if Linux
                sh 'matlab -batch "air_spring_script"'
            }
        }

        stage('Post-processing') {
            steps {
                echo 'MATLAB script finished.'
                // Optional: Archive any output files or plots
                archiveArtifacts artifacts: 'plots/**', allowEmptyArchive: true
            }
        }
    }
}
