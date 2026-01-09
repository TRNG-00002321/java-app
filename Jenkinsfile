pipeline{
    agent any

     // Environment variables for the pipeline
        environment {
            APP_NAME = 'calculator-app'
            APP_VERSION = '1.0.0'
            DOCKER_IMAGE = "${APP_NAME}"
            DOCKER_TAG = "${BUILD_NUMBER}"
        }


    // Tool configuration
    tools {
        maven 'Maven-3.9'  // Configure this in Jenkins Global Tool Configuration
    }

     stages {
            stage('Initialize') {
                steps {
                    echo '==========================================='
                    echo '   Jenkins Pipeline - Calculator Demo'
                    echo '==========================================='
                    echo "Application: ${APP_NAME} v${APP_VERSION}"
                    echo "Build Number: ${BUILD_NUMBER}"
                    echo "Environment: ${params.ENVIRONMENT}"
                    echo "Workspace: ${WORKSPACE}"
                    echo '==========================================='
                }
            }

        }
        
}