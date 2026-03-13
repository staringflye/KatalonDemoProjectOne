pipeline {
    agent any
    stages {
        stage('GetProjectFromSCM') {
            steps {
                echo 'Cloning projet from SCM'
                git branch: 'master', url: 'https://github.com/staringflye/KatalonDemoProjectOne'
            }
        }
        stage('Test') {
            steps {
                dir('/var/lib/jenkins/workspace/7_RunJenkinsfileFromSC_KatalonDockerRun'){
                    sh 'docker run -t --rm --shm-size=2g -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh -projectPath=/tmp/project -retry=0 -testSuitePath="Test Suites/Suite1" -browserType="Firefox" -executionProfile="default" -apiKey="d32dfcd7-8e90-4206-90d0-2e3560dbf7ea" -orgID=3320196 --config -webui.autoUpdateDrivers=true -webui.chrome.args="--no-sandbox,--disable-dev-shm-usage"'
                }
          }
      }
  }
  post {
    always {
      archiveArtifacts artifacts: 'Reports/**/*.*', fingerprint: true
      junit 'Reports/*/Suite1/*/*.xml'
    }
  } 
}
