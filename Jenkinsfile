node {
  properties([
    [$class: 'BuildBlockerProperty',
     blockLevel: 'GLOBAL',
     blockingJobs: '^.*-pipeline',
     scanQueueFor: 'ALL',
     useBuildBlocker: true],
   disableConcurrentBuilds(),
   [$class: 'BuildDiscarderProperty', 
      strategy: [
        $class: 'LogRotator', 
        daysToKeepStr: '10'
      ]
    ], [$class: 'ScannerJobProperty', doNotScan: false]
  ])

  stage('Checkout') {
    checkout scm
  }

  stage('Build') {
    steps {
      jobDsl targets: ['jobdsl/**/*.groovy'].join('\n'),
       removedJobAction: 'DELETE',
       removedViewAction: 'DELETE',
       lookupStrategy: 'SEED_JOB',
       ignoreExisting: false,
       sandbox: true,
       additionalClasspath: ['lib/*.jar','src/main/groovy'].join('\n')
    }
  }
}