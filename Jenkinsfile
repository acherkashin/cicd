pipeline {
  agent any

  stages {
    stage('Startup') {
      steps {
        script {
          sh 'npm install -g yarn'
          sh 'yarn install'
        }
      }
    }
    stage('Test') {
      steps {
        script {
          sh 'yarn test'
        }
      }
      post {
        always {
          publishHTML target: [
            allowMissing         : false,
            alwaysLinkToLastBuild: false,
            keepAll             : true,
            reportDir            : 'output/coverage/jest',
            reportFiles          : 'index.html',
            reportName           : 'Test Report'
          ]
        }
      }
    }
    stage('Build') {
      steps {
        script {
          sh 'yarn build'
        }
      }
    }
    // stage('Deploy') {
    //   when {
    //     expression {
    //       currentBuild.result == null || currentBuild.result == 'SUCCESS'
    //     }
    //   }
    //   steps {
    //     script {
        //   def server = Artifactory.server 'My_Artifactory'
        //   uploadArtifact(server)
    //     }
    //   }
    // }
  }
}

// def uploadArtifact(server) {
//   def uploadSpec = """{
//             "files": [
//               {
//                 "pattern": "continuous-test-code-coverage-guide*.tgz",
//                 "target": "npm-stable/"
//               }
//            ]
//           }"""
//   server.upload(uploadSpec)def buildInfo = Artifactory.newBuildInfo()
//   server.upload spec: uploadSpec, buildInfo: buildInfo
//   server.publishBuildInfo buildInfo
// }