pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('setup') {
      steps {
        sh 'mkdir -p ${CONTEXT}'
        sh 'mkdir -p ${MODULES}'
      }
    }
    stage('clone repos') {
      steps {
        parallel(
          "erp": {
            echo 'cloning ERP'
            sh '''if [ -d "${CONTEXT}" ]; then
  hg clone ${REPO_ERP}
else
  hg update -R ${CONTEXT}
fi
'''
            
          },
          "modules": {
            echo 'cloning modules'
            sh '''if [ -d "${CONTEXT}/${MODULES}/org.openbravo.util.db" ]; then
  hg clone ${REPO_MODULES} ${CONTEXT}/${MODULES}/org.openbravo.util.db
else
  hg update -R ${CONTEXT}/modules/org.openbravo.util.db
fi
'''
            
          }
        )
      }
    }
    stage('deliver') {
      steps {
        sh 'mv ${MODULES}/* ${CONTEXT}/${MODULES}/'
      }
    }
  }
  environment {
    WORKSPACE = pwd()
    CONTEXT = 'context'
    MODULES = 'modules'
    REPO_ERP = 'https://code.openbravo.com/erp/devel/pi'
    REPO_MODULES = 'https://code.openbravo.com/erp/mods/org.openbravo.util.db'
  }
}