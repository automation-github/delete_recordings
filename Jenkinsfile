pipeline {
  agent any
  stages {
    stage('test_npvr_recording_deletion_5.1') {
      agent any
      environment {
        target_cluster = '10.65.182.11'
        test_name = 'test_npvr_recording_deletion.py'
      }
      steps {
        sh '''set +e

ssh root@$target_cluster -t "pytest -r a -v -s /var/Nightswatch/CI_loops/CI_loop25/delete_recordings/$test_name" --junitxml="/tmp/delete_recordings/$test_name.xml"'''
      }
    }
    stage('test_rsdvr_recording_deletion_5.1') {
      agent any
      environment {
        target_cluster = '10.65.182.11'
        test_name = 'test_rsdvr_recording_deletion.py'
      }
      steps {
        sh '''set +e

ssh root@$target_cluster -t "pytest -r a -v -s /var/Nightswatch/CI_loops/CI_loop25/delete_recordings/$test_name" --junitxml="/tmp/delete_recordings/$test_name.xml"'''
      }
    }
    stage('delete_recordings_copy_xml') {
      agent any
      environment {
        target_custer = '10.65.182.11'
      }
      steps {
        sh 'scp -p root@$target_cluster:/tmp/delete_recordings/*.xml .'
      }
    }
    stage('publish_junit') {
      steps {
        junit(testResults: '*.xml', healthScaleFactor: 1, allowEmptyResults: true)
      }
    }
  }
}