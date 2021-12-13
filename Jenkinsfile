pipeline {
  agent any
  environment {
    APPSYSID = 'db4cfd171b98c1501c7a415de54bcb4f'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS = 'servicenow'
    DEVENV = 'https://hclnowintelligence.service-now.com/'
    TESTENV = 'https://hcltechdemosls4.service-now.com/'
    #PRODENV = 'https://prodinstance.service-now.com/'
    TESTSUITEID = 'bf8c266d732333005ce769972bf6a777'
  }
  stages {
    stage('Build') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", appSysId: "${APPSYSID}", obtainVersionAutomatically: true, url: "${DEVENV}")
      }
    }
    stage('Test') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}")
        snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
      }
    }
    
  }
}
