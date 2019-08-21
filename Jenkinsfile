pipeline {
  agent any
  stages {
    stage('hi') {
      steps {
        echo 'hello world'
      }
    }
    stage('Credentials') {
      steps {
        withCredentials(bindings: [[$class:  'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'Creds', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
          sh """
                                             mkdir -p ~/.aws
                                             echo "[default]" >~/.aws/credentials
                                             echo "[default]" >~/.boto
                                             echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.boto
                                             echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}" >>~/.boto
                                             echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.aws/credentials
                                             echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}" >>~/.aws/credentials
                                      """
        }
      }
    }
    stage('check index.html') {
      steps {
        sh """
                                             tidy -q -e index.html
                                      """
      }
    }
  }
}
