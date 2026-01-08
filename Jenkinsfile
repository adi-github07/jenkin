pipeline {
  agent any

  environment {
    ENV = "${env.JOB_NAME.contains('/prod/') ? 'prod' :
           env.JOB_NAME.contains('/test/') ? 'test' : 'dev'}"
  }

  stages {
    stage('Show Environment') {
      steps {
        echo "Job Name  : ${env.JOB_NAME}"
        echo "ENV picked: ${ENV}"
      }
    }

    stage('Approval (Prod only)') {
      when {
        expression { ENV == 'prod' }
      }
      steps {
        input message: "Approve PROD deployment?"
      }
    }

    stage('Dummy Deploy') {
      steps {
        echo "Deploying to ${ENV} environment"
      }
    }
  }
}
