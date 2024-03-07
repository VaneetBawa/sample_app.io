pipeline {
    agent any
    environment {
        LT_BUILD_NAME = "lambdatest-pipeline"
    }
    stages {
  stage('Setup') {
    steps {
      sh 'wget https://downloads.lambdatest.com/tunnel/v3/windows/64bit/LT_Windows.zip'
      sh 'sudo apt-get install zip unzip' 
      sh 'unzip -o LT_Windows.zip'
      sh './LT --user ${LT_USERNAME} --key ${LT_ACCESS_KEY} '
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
