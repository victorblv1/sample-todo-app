pipeline {
    agent any
    stages {
  stage('Setup') {
    steps {
      sh 'wget https://downloads.lambdatest.com/tunnel/v3/mac/64bit/LT_Mac.zip'
      sh 'unzip -o LT_Mac.zip'
      sh './LT --user ${LT_USERNAME} --key ${LT_ACCESS_KEY} --tunnelName jenkins-tunnel --infoAPIPort 8000 &'
    }
  }

  stage('Test') {
    steps {
      sh 'sleep 5'
      sh 'python3 -m http.server 8081 &'
      sh 'python3 test_sample_todo_app.py'
      sh 'pkill -f "http.server"'
      sh 'sleep 10'
      sh 'curl -X DELETE http://127.0.0.1:8000/api/v1.0/stop'
    }
  }

}
}
