pipeline {
    agent { label 'windows-agent' }

    // Parameters that can be set from Jenkins UI
    parameters {
        string(name: 'MASS', defaultValue: '500', description: 'Mass (kg)')
        string(name: 'STIFFNESS', defaultValue: '20000', description: 'Spring stiffness (N/m)')
        string(name: 'DAMPING', defaultValue: '1500', description: 'Damping coefficient (Ns/m)')
    }

    environment {
        MATLAB_PATH = 'C:\\Program Files\\MATLAB\\R2024b\\bin\\matlab.exe'
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
                echo "Running air_spring_script with parameters: M=${params.MASS}, K=${params.STIFFNESS}, C=${params.DAMPING}"
                bat "\"${MATLAB_PATH}\" -batch \"cd('${WORKSPACE_DIR}'); air_spring_script(${params.MASS}, ${params.STIFFNESS}, ${params.DAMPING})\""
            }
        }

        stage('Post-processing') {
            steps {
                echo 'Post-processing stage (if needed)'
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
