pipeline {
  agent any

  environment {
    ENV = "${env.JOB_NAME.contains('/prod/') ? 'prod' :
           env.JOB_NAME.contains('/test/') ? 'test' : 'dev'}"
  }

  stages {
    stage('Detect Environment') {
      steps {
        echo "Job Name: ${env.JOB_NAME}"
        echo "Detected ENV: ${ENV}"
      }
    }

    stage('Prod Approval') {
      when {
        expression { ENV == 'prod' }
      }
      steps {
        input message: 'Approve PROD execution?'
      }
    }

    stage('Dummy Step') {
      steps {
        echo "Running pipeline in ${ENV} environment"
      }
    }
  }
}
