pipeline {
  agent { docker { image 'node:20' } }

  triggers { cron('H 5 * * 1-5') }

  environment {
    CAMPUS_KEY = credentials('campus-key')
  }

  stages {
    stage('Install') {
      steps {
        sh 'npm install -g newman'
      }
    }
    stage('API tests') {
      steps {
        sh '''
          newman run collections/enrolment-rules.postman_collection.json \
            --env-var apiKey=$CAMPUS_KEY \
            -r cli,junit \
            --reporter-junit-export results/enrolment-rules.xml
        '''
      }
    }
  }

  post {
    always {
      junit 'results/*.xml'
    }
    failure {
      mail to: 'qa-team@example.com',
           subject: "API tests failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "See ${env.BUILD_URL}"
    }
  }
}
