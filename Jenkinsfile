pipeline {
    // Run on the Windows agent
    agent { label 'windows-agent' }

    environment {
        // Path to your MATLAB executable (Windows path, no surrounding quotes)
        MATLAB_PATH = 'C:\\Program Files\\MATLAB\\R2024b\\bin\\matlab.exe'
        
        // Path to your project workspace on the Windows agent
        WORKSPACE_DIR = 'F:\\A_rptu\\German_Resume\\jenkins_CI_Cd\\air_spring_system'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Checking out the Git repository...'
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'git@github.com:omrezkhan/air_spring_system.git']]])
            }
        }

        stage('Run MATLAB Script') {
            steps {
                echo 'Running air_spring_script.m'
                // Windows batch command to run MATLAB with proper quoting
                bat "\"${MATLAB_PATH}\" -batch \"cd('${WORKSPACE_DIR}'); air_spring_script\""
            }
        }

        stage('Post-processing') {
            steps {
                echo 'Post-processing stage (if needed)'
                // Add any post-processing commands here
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
