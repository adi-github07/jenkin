pipeline {
  agent any

  stages {

    stage('Detect Environment') {
      steps {
        script {
          if (env.JOB_NAME.contains('/prod/')) {
            env.ENV = 'prod'
          } else if (env.JOB_NAME.contains('/test/')) {
            env.ENV = 'test'
          } else {
            env.ENV = 'dev'
          }
        }

        echo "Job Name     : ${env.JOB_NAME}"
        echo "Detected ENV : ${env.ENV}"
      }
    }

    stage('Prod Approval') {
      when {
        expression { env.ENV == 'prod' }
      }
      steps {
        input message: 'Approve PROD execution?'
      }
    }

    stage('Dummy Step') {
      steps {
        echo "Running pipeline in ${env.ENV} environment"
      }
    }
  }
}
