pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  environment {
    WORKSPACE = pwd()
    CONTEXT = 'context'
    MODULES = 'modules'
    REPO_ERP = 'https://code.openbravo.com/erp/devel/pi'
    REPO_MODULES = 'https://code.openbravo.com/erp/mods/org.openbravo.util.db'
  }
  stages {
    stage('setup') {
      steps {
        sh 'mkdir -p ${CONTEXT}'
        sh 'mkdir -p ${MODULES}'         
      }
    }
  }  
  stages {
    stage('clone repos') {
      steps {
        parallel(
          "erp": {
            echo 'cloning ERP'
            sh 'hg clone ${REPO_ERP}'
          },
          "modules": {
            echo 'cloning modules'
            sh 'hg clone ${REPO_MODULES}'
          }
        )
      }
    }
  }
  stages {
    stage('deliver') {
      steps {
        sh 'mv ${MODULES}/* ${CONTEXT}/${MODULES}/'
      }
    }
  }  
}