pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('clone repos') {
      steps {
        echo 'some tests running'
        sh '''#!/usr/bin/env python
print ('hello from python')
print ('goodbye from python')
'''
      }
    }
  }
}