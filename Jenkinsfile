#!groovy

def target_cluster = "10.65.182.143"

def BuildJob(projectName) {
    try {
       stage(projectName) {
         node {      
           def res = build job:projectName, propagate: false
           result = res.result

           if (result.equals("SUCCESS")) {
           } else {
              error 'FAIL' //sh "exit 1" // this fails the stage
           }
         }
       }
    } catch (e) {
        currentBuild.result = 'UNSTABLE'
        result = "FAIL" // make sure other exceptions are recorded as failure too
    }
}

node {
  dir('/var/lib/jenkins/workspace/CI_LOOP3_5.1_SOLID_182.143') {

    stage('installation') {
      sh "python2.7 /var/tmp/Nightswatch/deploy/upgrade_machines_sa.py -p $target_cluster --ininame \'/var/lib/jenkins/nightswatch/5.1/config.ini\'"
    }

    BuildJob('multiple_pods/master')

    stage('copy xmls') {
      sh "scp -p root@$target_cluster:/tmp/multiple_pods/*.xml ."
    }

    stage('check_cores') {
      sh "ssh root@$target_cluster 'python2.7 /var/Nightswatch/deploy/find_cores.py'"
    }

    stage('publish junit results') {
      junit(testResults: '*.xml', healthScaleFactor: 1.0, allowEmptyResults: true)
    }
  }
}