pipeline {
  agent any
  stages {
    stage('multiple_pods_basic_functionality_5.1') {
      agent any
      environment {
        test_name = 'test_multiple_pods_basic_functionality.py'
      }
      steps {
        build(job: 'multiple_pods_basic_functionality_5.1', propagate: false)
      }
    }
    stage('multiple_pods_session_allocation_5.1') {
      agent any
      environment {
        test_name = 'test_multiple_pods_session_allocation.py'
      }
      steps {
        build(job: 'multiple_pods_session_allocation_5.1', propagate: false)
      }
    }
  }
  environment {
    target_cluster = '10.65.182.143'
  }
}
